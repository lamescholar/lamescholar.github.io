---
comments: true
title: Translation
---

In my opinion, [ChatGPT](/ru/chatgpt)'s most significant ability is ability to translate. Unlike Google Translate or Yandex Translate, ChatGPT translation is much more stable. However, ChatGPT itself has a number of disadvantages:

1) Length limit and message limit.

2) Not available in some regions.

3) Anytime OpenAI can make access paid.

Because of these disadvantages, a local, open source alternative to ChatGPT is needed. And it exists. How does it work? You insert the text into text.txt. You run the script. The script translates the text in chunks ("batches" of 3 sentences). As soon as the script translates a chunk of text, it displays a chunk of translation. Translation is gradually assembled in the command line. You can read translation as it happens. At the end, translation is saved into translation.txt.
<br><br>

<video width="100%" preload="auto" muted controls>
    <source src="/files/qwen3.mp4" type="video/mp4">
</video>
<br>

About the script. The script splits the text into paragraphs, and paragraphs into sentences. Each paragraph is split into chunks of 3 sentences, which are fed to the qwen3:4b model. I install it via Ollama.

3 sentences is optimal size. Too large a chunk may overload the model, break the translation. One sentence at a time - no context.
<br><br>

Before running the script, you need to have these **prerequisites**:

**Ollama** - <https://ollama.com/>

Download, then install **qwen3:4b** model:

```
ollama run qwen3:4b
```

**Python** - <https://www.python.org/downloads/>

Download, then install **nltk package** (to break down paragraphs into sentences):

```
pip install nltk
```
<br>

Now the script. I recommend you create a folder and hold all files in it.

```
import nltk
from nltk.tokenize import sent_tokenize
import subprocess
import re
import textwrap

# Download punkt tokenizer if not already present
try:
    nltk.data.find('tokenizers/punkt')
except LookupError:
    nltk.download('punkt')

# Config
input_file = 'text.txt'
output_file = 'translation.txt'

# Read and split text into paragraphs
with open(input_file, 'r', encoding='utf-8') as f:
    raw_text = f.read()

# Split paragraphs
paragraphs = [p.strip() for p in raw_text.split('\n\n') if p.strip()]

# Function to split paragraph into sentences
def split_into_sentences(text):
    return sent_tokenize(text)

# Generate batching rule
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
        if threes >= 1:
            return [3] * (threes - 1) + [2, 2]
        else:
            return [2, 2]
    elif remainder == 2:
        return [3] * threes + [2]

# Split paragraphs into batches
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

# Prepare batches
batches, paragraph_batch_counts = create_batches(paragraphs)
translated_paragraphs = [[] for _ in paragraphs]
batches_processed_per_paragraph = [0] * len(paragraphs)

print(f"🔄 Translating {len(batches)} batches...\n")

max_width = 80
line_length_by_paragraph = {}

# Process each batch
for (p_idx, batch) in batches:
    
    if len(batch.split()) < 3:
        translated = batch
    else:
        prompt = f"/no_think\n\nReturn only translation. Translate to English: {batch}"

        try:
            result = subprocess.run(
                ['ollama', 'run', 'qwen3:4b'],
                input=prompt,
                stdout=subprocess.PIPE,
                stderr=subprocess.PIPE,
                encoding='utf-8',
            )

            if result.returncode != 0:
                print(f"\n[ERROR] Batch failed:\nPrompt: {prompt}\nError: {result.stderr.strip()}")
                translated = '[TRANSLATION ERROR]'
            else:
                translated = re.sub(r'</?think>', '', result.stdout).strip()

        except Exception as e:
            print(f"\n[EXCEPTION] Batch failed:\nPrompt: {prompt}\nException: {str(e)}")
            translated = '[TRANSLATION ERROR]'

    translated_paragraphs[p_idx].append(translated)
    batches_processed_per_paragraph[p_idx] += 1

    current_length = line_length_by_paragraph.get(p_idx, 0)
    words = translated.split()

    for word in words:
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

# Write final translation to output file
with open(output_file, 'w', encoding='utf-8') as out:
    for paragraph_batches in translated_paragraphs:
        out.write(' '.join(paragraph_batches).strip() + '\n\n')

print("✅ Translation complete.")
```

I called it qwen3-visual.py, since it displays translated chunks in command line.
<br><br>

OK, you have in your folder:<br>
text.txt<br>
qwen3-visual.py

To easily run your script, create a .bat file.

qwen3-visual.bat:

```
python qwen3-visual.py
pause
```
<br>

Now you can create command-line translator.

translator.bat:

```
@echo off
chcp 65001 > nul
setlocal EnableDelayedExpansion

:loop
echo Enter/paste your text. End with a single dot (.) on a new line.

> text.txt echo(

:read
set "line="
set /p "line=> "
if "!line!"=="." goto process
>> text.txt echo(!line!
goto read

:process
echo Running translation...
python qwen3-visual.py
echo.
goto loop
```