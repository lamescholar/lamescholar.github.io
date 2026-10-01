---
layout: page
title: OCR
---

Language model:<br>
<https://huggingface.co/mradermacher/LightOnOCR-2-1B-GGUF/tree/main>
<br><br>

ocr.py:

```python
import base64
import requests
import subprocess
import time
import sys

SERVER_URL = "http://localhost:8080/v1/chat/completions"
HEALTH_URL = "http://localhost:8080/health"
LIST_FILE = "images.txt"
OUTPUT_FILE = "ocr.txt"

LLAMA_CMD = [
    "llama-server",
    "-m", "LightOnOCR-2-1B-Q4_K_M.gguf",
    "--mmproj", "mmproj-F16.gguf",
    "-c", "4096",
    "-t", "4",
    "--temp", "0"
]

def wait_for_server(timeout: int = 60) -> bool:
    start_time = time.time()
    while time.time() - start_time < timeout:
        try:
            res = requests.get(HEALTH_URL, timeout=2)
            if res.status_code == 200:
                return True
        except requests.RequestException:
            pass
        time.sleep(1)
    return False

def ocr_image(image_path: str) -> str:
    with open(image_path, "rb") as f:
        b64_image = base64.b64encode(f.read()).decode("utf-8")

    payload = {
        "messages": [
            {
                "role": "user",
                "content": [
                    {
                        "type": "text",
                        "text": "Transcribe all text from this image exactly as written. Use LaTeX for math notation. Output only the text."
                    },
                    {
                        "type": "image_url",
                        "image_url": {
                            "url": f"data:image/png;base64,{b64_image}"
                        }
                    }
                ]
            }
        ]
    }

    res = requests.post(SERVER_URL, json=payload)
    res.raise_for_status()
    return res.json()["choices"][0]["message"]["content"]

def main():
    server_process = None
    try:
        server_process = subprocess.Popen(LLAMA_CMD, stdout=subprocess.DEVNULL, stderr=subprocess.DEVNULL)
        if not wait_for_server(60):
            print("Error: Server failed to start.")
            sys.exit(1)

        with open(LIST_FILE, "r", encoding="utf-8") as f:
            image_paths = [line.strip() for line in f if line.strip()]

        with open(OUTPUT_FILE, "a", encoding="utf-8") as out_f:
            for index, path in enumerate(image_paths, start=1):
                print(f"[{index}/{len(image_paths)}] {path}")
                try:
                    out_f.write(ocr_image(path) + "\n")
                    out_f.flush()
                except Exception as e:
                    print(f"Error {path}: {e}")
                    
        print(f"\nDone!")

    finally:
        if server_process:
            server_process.terminate()
            try:
                server_process.wait(timeout=10)
            except subprocess.TimeoutExpired:
                server_process.kill()

if __name__ == "__main__":
    main()
```
<br>

```
cd <path to folder>
find "$PWD" -maxdepth 1 -type f -name "*.jpg" | sort -V > images.txt
rm ocr.txt
python ocr.py
```
