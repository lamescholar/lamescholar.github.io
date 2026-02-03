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

Insert the text into a text file, then run the script. The script translates the text chunk by chunk. As soon as the script translates a chunk of text, it displays a translation. You can read translation as it happens. At the end, full translation goes into translation.txt.
<br><br>

<video width="100%" preload="auto" muted controls>
    <source src="/files/qwen3.mp4" type="video/mp4">
</video>
<br>

How the script works? First, it splits the text into paragraphs, then paragraphs into sentences. Why? Paragraph is usually too big to translate all at once. For this reason, each paragraph is split into batches of 3 sentences. This way, model can translate a large text batch by batch.

3 sentences is the optimal size. Too large a chunk overloads the model and breaks the translation. But also, it can't be too small. If you translate sentence by sentence, the context is lost.

At the moment, I found two Small Language Models that do English translation well: Qwen3-4B and TranslateGemma-4B.
<br><br>

Before running the script, you need to have these **prerequisites**:

**llama.cpp** - <https://github.com/ggml-org/llama.cpp/releases>

**translategemma-4b-it.Q4_K_M** - <https://huggingface.co/mradermacher/translategemma-4b-it-GGUF/tree/main>

**Python** - <https://www.python.org/downloads/>

Install **nltk package** (to split paragraphs into sentences):

```
pip install nltk
```
<br>

Now the script.

Create a folder. Store all files in this folder.

Create translategemma-visual.py:

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
MODEL_PATH = r'llama-b6715-bin-win-cpu-x64\translategemma-4b-it.Q4_K_M.gguf'

MODEL_PARAMS = {
    "repeat_penalty": 1.0,
    "temperature": 0.6,
    "top_k": 20,
    "top_p": 0.95,
}

SERVER_ARGS = [
    "-m", MODEL_PATH,
    "--port", "8080",
    "--host", "127.0.0.1",
    "--threads", "4"
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
        f"<|im_start|>user\nReturn only translation. Translate to English:\n{batch_text}\n<|im_end|>\n"
        f"<|im_start|>assistant\n"
    )

    payload = {
        "prompt": prompt_text,
        "repeat_penalty": MODEL_PARAMS['repeat_penalty'],
        "temperature": MODEL_PARAMS['temperature'],
        "top_k": MODEL_PARAMS['top_k'],
        "top_p": MODEL_PARAMS['top_p'],
        "stop": ["<|im_end|>"],
        "stream": False
    }

    try:
        response = requests.post(LLAMA_SERVER_URL, json=payload, timeout=600)
        response.raise_for_status()
        data = response.json()
        translated = data.get('content', '').strip()
        for token in ["<|im_end|>", "</s>", "[end of text]"]:
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

OK, you have in your folder:<br>
llama-b6715-bin-win-cpu-x64<br>
llama-b6715-bin-win-cpu-x64\translategemma-4b-it.Q4_K_M<br>
text.txt<br>
translategemma-visual.py

To easily run your script, create .bat file.

translategemma-visual.bat:

```
python translategemma-visual.py
pause
```
<br>

If you want to see only the progress bar, here you go:

[translategemma.py](/files/translategemma.py)
<br><br>

Simple command-line translator.

translator.bat:

```
@echo off
chcp 65001 > nul
setlocal EnableDelayedExpansion

:loop
echo Enter your text. End with a single dot (.) on a new line.

> text.txt echo(

:read
set "line="
set /p "line=> "
if "!line!"=="." goto process
>> text.txt echo(!line!
goto read

:process
echo Running translation...
python translategemma-visual.py
echo.
goto loop
```

Create a shortcut on your Desktop.