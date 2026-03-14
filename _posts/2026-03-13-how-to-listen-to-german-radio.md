---
layout: post
tag: Posts
comments: true
title: How to listen to German radio
---

2026-03-13

# How to listen to German radio
<br>

Now is the golden age of language learning. Small language models are lightweight and free, your laptop can run them. These models can transcribe and translate European languages. You can download MP3 file of [Deutchlandfunk Kultur](https://www.deutschlandfunkkultur.de/) broadcast, transcribe it with [whisper](/en/whisper), translate it with [Qwen3-4B](/en/machine-translation) and build a PDF with transcript and translation. Then you can listen to broadcast, see the transcript and translation, pause ([Winamp](https://sourceforge.net/projects/winamp/) has global hotkeys, Ctrl+Space and Ctrl+Left work great for me), look up a word in the [dictionary](/en/dictionaries).

Here's the script that translates the transcript and outputs parallel_translation.pdf:

`pip install fpdf2 nltk`

```
import nltk
from nltk.tokenize import sent_tokenize
import requests
import subprocess
import time
import os
import sys
from tqdm import tqdm
from fpdf import FPDF

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
    "--port", "8080",
    "--host", "127.0.0.1",
    "--threads", "4"
]
SERVER_STARTUP_TIMEOUT = 300

input_file = 'text.txt'
output_pdf = 'parallel_translation.pdf'

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

        print(f"ERROR: Server failed to start within {SERVER_STARTUP_TIMEOUT}s.")
        if server_process.poll() is None:
            server_process.terminate()
        return None

    except Exception as e:
        print(f"FATAL ERROR: Could not start server process: {e}")
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
    else:
        return [3] * threes + [2]

def create_batches(paragraphs):
    batches = []
    for p_idx, paragraph in enumerate(paragraphs):
        sentences = split_into_sentences(paragraph)
        n = len(sentences)
        if n == 0:
            continue
        rule = generate_batching_rule(n)
        pointer = 0
        for size in rule:
            batch = " ".join(sentences[pointer:pointer + size])
            batches.append((p_idx, batch))
            pointer += size
    return batches

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

# setup
pdf = FPDF()
pdf.set_auto_page_break(auto=True, margin=15)
pdf.add_page()

# font
pdf.add_font("Arial", style="", fname="C:/Windows/Fonts/arial.ttf")
pdf.set_font('Arial', size=11)

# layout
margin = 15
gutter = 10
col_width = (pdf.w - (margin * 2) - gutter) / 2
line_height = 6

try:
    try:
        with open(input_file, 'r', encoding='utf-8') as f:
            raw_text = f.read()
    except FileNotFoundError:
        print(f"Error: Input file '{input_file}' not found.")
        sys.exit(1)

    paragraphs = [p.strip() for p in raw_text.split('\n\n') if p.strip()]
    batches = create_batches(paragraphs)

    print(f"🔄 Translating {len(batches)} batches...\n")

    if not is_server_ready():
        server_process = start_server()
        if server_process is None:
            sys.exit(1)

    for (p_idx, left_txt) in tqdm(batches, desc="Processing", unit="batch"):
        if len(left_txt.split()) < 3:
            right_txt = left_txt
        else:
            right_txt = translate_batch_with_server(left_txt)
        
        # calculate the height needed for both sides
        # split_lines() helps us predict how many lines fpdf will create
        lines_left = pdf.multi_cell(col_width, line_height, left_txt, dry_run=True, output="LINES")
        lines_right = pdf.multi_cell(col_width, line_height, right_txt, dry_run=True, output="LINES")
        
        max_lines = max(len(lines_left), len(lines_right))
        row_height = max_lines * line_height + 4 # +4 for internal padding

        # check for page break
        if pdf.get_y() + row_height > pdf.page_break_trigger:
            pdf.add_page()

        start_x = pdf.get_x()
        start_y = pdf.get_y()

        # draw the border
        pdf.rect(start_x, start_y, pdf.w - (margin * 2), row_height)
        
        # draw the middle line
        pdf.line(start_x + col_width + (gutter/2), start_y, 
                 start_x + col_width + (gutter/2), start_y + row_height)

        # place the text
        pdf.set_xy(start_x + 2, start_y + 2) # +2 for padding inside box
        pdf.multi_cell(col_width, line_height, left_txt, border=0, align='L')
        
        pdf.set_xy(start_x + col_width + gutter, start_y + 2)
        pdf.multi_cell(col_width, line_height, right_txt, border=0, align='L')

        # move cursor to the bottom of the common box
        pdf.set_y(start_y + row_height)

    pdf.output(output_pdf)
    print(f"\n✅ Translation complete.")

finally:
    if server_process:
        if server_process.poll() is None:
            server_process.terminate()
            try:
                server_process.wait(timeout=5)
            except subprocess.TimeoutExpired:
                server_process.kill()
```