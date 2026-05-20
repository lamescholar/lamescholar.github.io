---
layout: page
title: Локальный переводчик
---

Языковая модель:

<https://huggingface.co/t-tech/T-lite-it-2.1-GGUF>
<br><br>

llama-cpp:

`yay -S llama.cpp`
<br><br>

```
python -m venv venv
source venv/bin/activate
pip install requests nltk PySide6
```
<br>

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

# configuration
LLAMA_SERVER_URL = "http://127.0.0.1:8080/completion"
SERVER_EXECUTABLE_PATH = '/usr/bin/llama-server'
MODEL_PATH = 'T-lite-it-2.1-Q4_K_M.gguf'

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

BATCH_TOKEN_TARGET = 90
BATCH_TOKEN_MIN = 50

# worker
class TranslationWorker(QThread):
    progress = Signal(int)
    status_msg = Signal(str)
    chunk_done = Signal(str, bool)
    finished = Signal()
    error = Signal(str)

    def __init__(self, text):
        super().__init__()
        self.raw_text = text
        self.server_process = None

    def run(self):
        try:
            try:
                nltk.data.find('tokenizers/punkt')
            except LookupError:
                nltk.download('punkt', quiet=True)
                nltk.download('punkt_tab', quiet=True)

            if not self.is_server_ready():
                self.status_msg.emit("Запуск llama-server...")
                self.server_process = self.start_server()
                if not self.server_process:
                    self.error.emit(f"Failed to launch server at {SERVER_EXECUTABLE_PATH}")
                    return

            paragraphs = [p.strip() for p in re.split(r'\n\s*\n', self.raw_text) if p.strip()]
            batches = self.create_batches(paragraphs)
            self.status_msg.emit(f"Куски: {len(batches)}")
            
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
                
            self.finished.emit()

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
    
    # batching functions
    @staticmethod
    def estimate_tokens(text):
        return int(len(text.split()) * 1.3)
             
    @staticmethod
    def create_batches(paragraphs):
        batches = []
    
        for p_idx, paragraph in enumerate(paragraphs):
            sentences = sent_tokenize(paragraph)
            
            if not sentences:
                continue
            
            sentence_sizes = [TranslationWorker.estimate_tokens(s) for s in sentences]
            total_paragraph_tokens = sum(sentence_sizes)
            
            current_batch_sentences = []
            current_batch_tokens = 0
            processed_tokens = 0
    
            for idx, sentence in enumerate(sentences):
                sentence_tokens = sentence_sizes[idx]
                remaining_tokens_in_paragraph = total_paragraph_tokens - processed_tokens
                if current_batch_sentences and (current_batch_tokens + sentence_tokens > BATCH_TOKEN_TARGET):
                    if remaining_tokens_in_paragraph < BATCH_TOKEN_MIN:
                        pass 
                    else:
                        batches.append((p_idx, " ".join(current_batch_sentences)))
                        current_batch_sentences = []
                        current_batch_tokens = 0
                current_batch_sentences.append(sentence)
                current_batch_tokens += sentence_tokens
                processed_tokens += sentence_tokens
                
            if current_batch_sentences:
                batches.append((p_idx, " ".join(current_batch_sentences)))

        return batches

    def translate_batch_api(self, batch_text):
        prompt_text = (
            f"<|im_start|>user\nТы - переводчик. Не переводи буквально. Выбирай выражения на русском. Верни только перевод.\nПереведи на русский:\n{batch_text}\n<|im_end|>\n"
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
            content = res.json().get('content', '').strip()
            content = re.sub(r'<think>', '', content, flags=re.DOTALL)
            content = re.sub(r'</think>', '', content, flags=re.DOTALL)
            content = re.sub(r'>', '', content, flags=re.DOTALL)
            return content.strip()
        except Exception as e:
            return f"[Error: {str(e)[:20]}]"

    def cleanup_server(self):
        if self.server_process:
            self.server_process.terminate()

class TranslatorApp(QMainWindow):
    def __init__(self):
        super().__init__()
        self.setWindowTitle("Локальный переводчик")
        self.resize(1000, 655)

        container = QWidget()
        self.main_layout = QVBoxLayout(container)
        self.editor_layout = QHBoxLayout()
        self.editor_layout.setSpacing(0)

        input_container = QWidget()
        input_layout = QVBoxLayout(input_container)
        input_layout.addWidget(QLabel("Ввод:"))
        self.input_area = QTextEdit()
        self.input_area.setAcceptRichText(False)
        input_layout.addWidget(self.input_area)

        output_container = QWidget()
        output_layout = QVBoxLayout(output_container)
        output_layout.addWidget(QLabel("Вывод:"))
        self.output_area = QTextEdit()
        self.output_area.setReadOnly(True)
        output_layout.addWidget(self.output_area)

        self.editor_layout.addWidget(input_container)
        self.editor_layout.addWidget(output_container)

        self.progress_bar = QProgressBar()
        self.status_label = QLabel("Готово")
        self.btn = QPushButton("Перевести")
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
        self.status_label.setText("Успех")
        self.btn.setEnabled(True)
        
    def closeEvent(self, event):
        if hasattr(self, 'worker') and self.worker.isRunning():
            self.worker.cleanup_server()
            self.worker.terminate()
            self.worker.wait()
        event.accept()

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
