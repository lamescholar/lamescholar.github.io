---
layout: page
comments: true
title: Machine translation
---

Since 2022, machine translation had a boost. ChatGPT produces decent translations. Unlike Google Translate, ChatGPT is very stable. However, ChatGPT has a number of disadvantages:

1) Usage limit.<br>
2) Not available in some regions.<br>
3) Any time OpenAI can close the free access.

It is much better to have a local, open source alternative to ChatGPT, and it actually exists. Here's how to use it:

Insert the text into a text file. Run the script. The script translates the text chunk by chunk. You can read translation as it happens. At the end, full translation goes into translation.txt.
<br><br>

<video width="100%" preload="auto" muted controls>
    <source src="/files/qwen3.mp4" type="video/mp4">
</video>
<br>

What is happening under the hood? First, the script splits the text into paragraphs, then paragraphs into sentences. Why? A paragraph can be too long to translate all at once. To avoid an overflow, paragraphs are split into batches of 3 sentences.
<br><br>

Before you can run the script, here's the **prerequisites**:

**llama.cpp** - <https://github.com/ggml-org/llama.cpp/releases>

**Qwen3-4B-Instruct-2507-Q4_K_M** - <https://huggingface.co/unsloth/Qwen3-4B-Instruct-2507-GGUF/tree/main>

**Python** - <https://www.python.org/downloads/>

Install **nltk package** (to split paragraphs into sentences):

```
pip install nltk
```
<br>

Now the script.

Create a folder. Store all files in this folder.

Create qwen3-visual.py:

```
import nltk
from nltk.tokenize import sent_tokenize
import requests
import subprocess
import time
import os
import sys
import re

# Configuration
LLAMA_SERVER_URL = "http://127.0.0.1:8080/completion"
SERVER_EXECUTABLE_PATH = r'llama-b6715-bin-win-cpu-x64\llama-server.exe'
MODEL_PATH = r'llama-b6715-bin-win-cpu-x64\Qwen3-4B-Instruct-2507-Q4_K_M.gguf'

MODEL_PARAMS = {
    "repeat_penalty": 1.0,
    "temperature": 0.6,
    "top_k": 20,
    "top_p": 0.95,
}

SERVER_ARGS = [
    "-m", MODEL_PATH,
    "-c", "4096",
    "-t", "4",
    "--port", "8080",
    "--host", "127.0.0.1"
]
SERVER_STARTUP_TIMEOUT = 300

input_file = 'text.txt'
output_file = 'translation.txt'

# nltk
def ensure_nltk_punkt():
    try:
        nltk.data.find('tokenizers/punkt')
    except LookupError:
        nltk.download('punkt', quiet=True)

# Server functions
def is_server_ready():
    try:
        payload = {"prompt": "Hello", "n_predict": 1, "stream": False}
        response = requests.post(LLAMA_SERVER_URL, json=payload, timeout=5)
        return response.status_code == 200
    except requests.exceptions.RequestException:
        return False

def start_server():
    if not os.path.exists(SERVER_EXECUTABLE_PATH):
        print(f"FATAL ERROR: Server executable not found at '{SERVER_EXECUTABLE_PATH}'")
        return None
    if not os.path.exists(MODEL_PATH):
        print(f"FATAL ERROR: Model file not found at '{MODEL_PATH}'")
        return None

    try:
        server_process = subprocess.Popen(
            [SERVER_EXECUTABLE_PATH] + SERVER_ARGS,
            stdout=subprocess.PIPE,
            stderr=subprocess.PIPE,
            text=True
        )

        for _ in range(SERVER_STARTUP_TIMEOUT):
            if is_server_ready():
                return server_process
            time.sleep(1)

        print(f"FATAL ERROR: Server failed to become ready within {SERVER_STARTUP_TIMEOUT}s.")
        if server_process.poll() is None:
            server_process.terminate()
        return None

    except Exception as e:
        print(f"FATAL ERROR: Could not start server process: {e}")
        if server_process and server_process.poll() is None:
            server_process.terminate()
        return None

# Batching functions
def split_into_sentences(text):
    return sent_tokenize(text)

def generate_batching_rule(n):
    if n < 1:
        return []
    if n == 1:
        return [1]
    threes = n // 3
    remainder = n % 3
    if remainder == 0:
        return [3] * threes
    elif remainder == 1:
        return [3] * (threes - 1) + [2, 2] if threes >= 1 else [2, 2]
    else:  # remainder == 2
        return [3] * threes + [2]

def create_batches(paragraphs):
    batches = []
    paragraph_batch_counts = []
    for p_idx, paragraph in enumerate(paragraphs):
        sentences = split_into_sentences(paragraph)
        n = len(sentences)
        if n == 0:
            paragraph_batch_counts.append(0)
            continue
        rule = generate_batching_rule(n)
        pointer = 0
        batch_count = 0
        for size in rule:
            batch = " ".join(sentences[pointer:pointer + size])
            batches.append((p_idx, batch))
            pointer += size
            batch_count += 1
        paragraph_batch_counts.append(batch_count)
    return batches, paragraph_batch_counts

# llama.cpp server API
def translate_batch_with_server(batch_text):
    prompt_text = (
        f"<|im_start|>user\nReturn only translation. Translate to English: {batch_text}\n<|im_end|>\n"
        f"<|im_start|>assistant\n"
    )

    payload = {
        "prompt": prompt_text,
        "repeat_penalty": MODEL_PARAMS['repeat_penalty'],
        "temperature": MODEL_PARAMS['temperature'],
        "top_k": MODEL_PARAMS['top_k'],
        "top_p": MODEL_PARAMS['top_p'],
        "stop": ["<|im_end|>", "<|file_separator|>"],
        "stream": False
    }

    try:
        response = requests.post(LLAMA_SERVER_URL, json=payload, timeout=600)
        response.raise_for_status()
        data = response.json()
        translated = data.get('content', '').strip()
        for token in ["<|im_end|>", "<|file_separator|>"]:
            translated = translated.replace(token, "").strip()
        return translated
    except requests.exceptions.ConnectionError:
        print(f"\n[ERROR] Connection failed. Is the server running at {LLAMA_SERVER_URL}?")
        return '[CONNECTION ERROR]'
    except requests.exceptions.RequestException as e:
        print(f"\n[ERROR] Request failed: {e}")
        return '[REQUEST ERROR]'
    except Exception as e:
        print(f"\n[EXCEPTION] Batch failed: {str(e)}")
        return '[TRANSLATION ERROR]'

server_process = None
ensure_nltk_punkt()

try:
    try:
        with open(input_file, 'r', encoding='utf-8') as f:
            raw_text = f.read()
    except FileNotFoundError:
        print(f"Error: Input file '{input_file}' not found.")
        sys.exit(1)

    paragraphs = [p.strip() for p in re.split(r'\n\s*\n', raw_text) if p.strip()]

    if not is_server_ready():
        server_process = start_server()
        if server_process is None:
            sys.exit(1)

    batches, paragraph_batch_counts = create_batches(paragraphs)
    translated_paragraphs = [[] for _ in paragraphs]
    batches_processed_per_paragraph = [0] * len(paragraphs)

    print(f"🔄 Translating {len(batches)} batches...\n")

    max_width = 80
    line_length_by_paragraph = {}

    for (p_idx, batch) in batches:
        if len(batch.split()) < 3:
            translated = batch
        else:
            translated = translate_batch_with_server(batch)

        translated_paragraphs[p_idx].append(translated)
        batches_processed_per_paragraph[p_idx] += 1

        current_length = line_length_by_paragraph.get(p_idx, 0)
        for word in translated.split():
            if current_length + len(word) + 1 > max_width:
                print()
                print(word, end=' ', flush=True)
                current_length = len(word) + 1
            else:
                print(word, end=' ', flush=True)
                current_length += len(word) + 1
        line_length_by_paragraph[p_idx] = current_length

        if batches_processed_per_paragraph[p_idx] == paragraph_batch_counts[p_idx]:
            print('\n')
            line_length_by_paragraph[p_idx] = 0

    with open(output_file, 'w', encoding='utf-8') as out:
        for paragraph_batches in translated_paragraphs:
            out.write(' '.join(paragraph_batches).strip() + '\n\n')

    print("✅ Translation complete.")

finally:
    if server_process:
        if server_process.poll() is None:
            server_process.terminate()
            try:
                server_process.wait(timeout=5)
            except subprocess.TimeoutExpired:
                print("Server did not terminate gracefully, forcing kill.")
                server_process.kill()
            server_process.stdout.close()
            server_process.stderr.close()
        else:
            print(f"\nServer process already terminated with return code {server_process.returncode}.")
```
<br>

Now you should have in your folder:<br>
llama-b6715-bin-win-cpu-x64<br>
llama-b6715-bin-win-cpu-x64\Qwen3-4B-Instruct-2507-Q4_K_M.gguf<br>
text.txt<br>
qwen3-visual.py

To quickly run your script, create .bat file.

qwen3-visual.bat:

```
python qwen3-visual.py
pause
```
<br>

If you want to see only the progress bar, here you go:

[qwen3.py](/files/qwen3.py)
<br><br>

translator.py:

```
import sys
import os
import re
import time
import subprocess
import requests
import nltk
from nltk.tokenize import sent_tokenize
from PySide6.QtWidgets import (
    QApplication, QMainWindow, QWidget,
    QVBoxLayout, QHBoxLayout,
    QPushButton, QTextEdit, QProgressBar,
    QLabel
)
from PySide6.QtCore import QThread, Signal, Qt

# Configuration
LLAMA_SERVER_URL = "http://127.0.0.1:8080/completion"
SERVER_EXECUTABLE_PATH = '/usr/bin/llama-server'
MODEL_PATH = 'Qwen3-4B-Instruct-2507-Q4_K_M.gguf'

MODEL_PARAMS = {
    "repeat_penalty": 1.0,
    "temperature": 0.6,
    "top_k": 20,
    "top_p": 0.95,
}

SERVER_ARGS = [
    "-m", MODEL_PATH,
    "-c", "4096",
    "-t", "4",
    "--port", "8080",
    "--host", "127.0.0.1"
]
SERVER_STARTUP_TIMEOUT = 300

class TranslationWorker(QThread):
    progress = Signal(int)
    status_msg = Signal(str)
    chunk_done = Signal(str, bool)
    finished = Signal(str)
    error = Signal(str)

    def __init__(self, text):
        super().__init__()
        self.raw_text = text
        self.server_process = None

    def run(self):
        try:
            self.status_msg.emit("Initializing NLTK...")
            try:
                nltk.data.find('tokenizers/punkt')
            except LookupError:
                nltk.download('punkt', quiet=True)
                nltk.download('punkt_tab', quiet=True)

            if not self.is_server_ready():
                self.status_msg.emit("Launching llama-server...")
                self.server_process = self.start_server()
                if not self.server_process:
                    self.error.emit(f"Failed to launch server at {SERVER_EXECUTABLE_PATH}")
                    return

            paragraphs = [p.strip() for p in re.split(r'\n\s*\n', self.raw_text) if p.strip()]
            batches = self.create_batches(paragraphs)
            
            self.status_msg.emit(f"Translating {len(batches)} batches...")
            
            last_p_idx = -1

            for i, (p_idx, batch_text) in enumerate(batches):
                is_new_paragraph = (p_idx != last_p_idx)
                
                if len(batch_text.split()) < 2:
                    translated = batch_text
                else:
                    translated = self.translate_batch_api(batch_text)
                
                self.chunk_done.emit(translated + " ", is_new_paragraph)
                
                last_p_idx = p_idx
                self.progress.emit(int(((i + 1) / len(batches)) * 100))

            self.finished.emit("Complete")

        except Exception as e:
            self.error.emit(f"Worker Exception: {str(e)}")
        finally:
            self.cleanup_server()

    def is_server_ready(self):
        try:
            r = requests.get("http://127.0.0.1:8080/health", timeout=2)
            return r.status_code == 200
        except:
            return False

    def start_server(self):
        if not os.path.exists(MODEL_PATH):
            return None
            
        proc = subprocess.Popen(
            [SERVER_EXECUTABLE_PATH] + SERVER_ARGS,
            stdout=subprocess.DEVNULL, stderr=subprocess.DEVNULL
        )
        
        for _ in range(SERVER_STARTUP_TIMEOUT):
            if self.is_server_ready():
                return proc
            time.sleep(1)
        return None

    def create_batches(self, paragraphs):
        batches = []
        for p_idx, paragraph in enumerate(paragraphs):
            sentences = sent_tokenize(paragraph)
            for i in range(0, len(sentences), 3):
                batch = " ".join(sentences[i:i+3])
                batches.append((p_idx, batch))
        return batches

    def translate_batch_api(self, batch_text):
        prompt_text = (
            f"<|im_start|>user\nReturn only translation. Translate to English: {batch_text}\n<|im_end|>\n"
            f"<|im_start|>assistant\n"
        )
        
        payload = {
            "prompt": prompt_text,
            "repeat_penalty": MODEL_PARAMS['repeat_penalty'],
            "temperature": MODEL_PARAMS['temperature'],
            "top_k": MODEL_PARAMS['top_k'],
            "top_p": MODEL_PARAMS['top_p'],
            "stop": ["<|im_end|>", "<|file_separator|>"],
            "stream": False
        }
        
        try:
            res = requests.post(LLAMA_SERVER_URL, json=payload, timeout=120)
            res.raise_for_status()
            return res.json().get('content', '').strip()
        except Exception as e:
            return f"[Error: {str(e)[:20]}]"

    def cleanup_server(self):
        if self.server_process:
            self.server_process.terminate()

class TranslatorApp(QMainWindow):
    def __init__(self):
        super().__init__()
        self.setWindowTitle("Local Translator")
        self.resize(1000, 655)

        container = QWidget()
        self.main_layout = QVBoxLayout(container)
        self.editor_layout = QHBoxLayout()
        self.editor_layout.setSpacing(0)

        input_container = QWidget()
        input_layout = QVBoxLayout(input_container)
        input_layout.addWidget(QLabel("Input:"))
        self.input_area = QTextEdit()
        self.input_area.setAcceptRichText(False)
        input_layout.addWidget(self.input_area)

        output_container = QWidget()
        output_layout = QVBoxLayout(output_container)
        output_layout.addWidget(QLabel("Output:"))
        self.output_area = QTextEdit()
        self.output_area.setReadOnly(True)
        output_layout.addWidget(self.output_area)

        self.editor_layout.addWidget(input_container)
        self.editor_layout.addWidget(output_container)

        self.progress_bar = QProgressBar()
        self.status_label = QLabel("Ready")
        self.btn = QPushButton("Translate")
        self.btn.clicked.connect(self.start)

        self.main_layout.addLayout(self.editor_layout)
        self.main_layout.addWidget(self.progress_bar)
        self.main_layout.addWidget(self.status_label)
        self.main_layout.addWidget(self.btn)

        self.setCentralWidget(container)

    def start(self):
        text = self.input_area.toPlainText().strip()
        if not text:
            return

        self.btn.setEnabled(False)
        self.output_area.clear()
        self.progress_bar.setValue(0)
        self.status_label.setText("Starting...")

        self.worker = TranslationWorker(text)
        self.worker.status_msg.connect(self.status_label.setText)
        self.worker.progress.connect(self.progress_bar.setValue)
        self.worker.chunk_done.connect(self.on_chunk_done)
        self.worker.error.connect(self.on_error)
        self.worker.finished.connect(self.on_finish)
        self.worker.start()

    def on_chunk_done(self, text, is_new_paragraph):
        if is_new_paragraph and self.output_area.toPlainText().strip():
            self.output_area.insertPlainText("\n\n")
        
        self.output_area.insertPlainText(text)
        self.output_area.verticalScrollBar().setValue(
            self.output_area.verticalScrollBar().maximum()
        )

    def on_error(self, msg):
        self.status_label.setText(msg)
        self.btn.setEnabled(True)

    def on_finish(self):
        self.status_label.setText("Success")
        self.btn.setEnabled(True)

if __name__ == "__main__":
    app = QApplication(sys.argv)
    
    app.setStyleSheet("""
        QTextEdit {
            border: 1px solid #c0c0c0;
            border-radius: 4px;
            padding: 8px;
        }
        QPushButton {
            padding: 10px;
            border: 1px solid #c0c0c0;
            border-radius: 4px;
        }
    """)
    
    from PySide6.QtGui import QFont
    app.setFont(QFont("Adwaita Sans", 13))
    
    window = TranslatorApp()
    window.show()
    sys.exit(app.exec())
```
