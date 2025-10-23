---
layout: page
comments: true
title: whisper
---

whisper is a program for speech recognition.
<br><br>

<https://github.com/openai/whisper>
<br><br>

Requirements to install:

* ffmpeg:

	Chocolatey - <https://chocolatey.org/install>

	Open a command prompt with administrator rights. Right-click on the Start button. Terminal (Administrator).

	`choco install ffmpeg`

* Python - <https://www.python.org/downloads/>

	Tick Add python.exe to PATH while downloading Python.
<br><br>

Installation:

Win+R cmd

`pip install -U openai-whisper`
<br><br>

Script for transript:

```
import whisper

model = whisper.load_model("base")
options = whisper.DecodingOptions(language="ru")
result = model.transcribe(r"path to the media file")

with open("transcript.txt", "w", encoding="utf-8") as txt:
    txt.write(result["text"])
```

Create text file, insert code, close. Change the name to w, the extension to .py.

Create folder named whisper. Place w.py in it.
<br><br>

Usage:

In w.py (open it with Notepad) in line

audio = whisper.load_audio("name of the media file with extension")

insert name of the media file with extension.

In line

result = model.transcribe(r"path to the media file")

insert path to the media file.

Set up language in this line:

options = whisper.DecodingOptions(language="ru")

Win+R cmd

`python path-to-whisper-folder\w.py`
<br><br>

#### subsai

<https://github.com/abdeladim-s/subsai>

subsai is version of whisper to creat subtitles

Installation:

`pip install git+https://github.com/abdeladim-s/subsai`

Python script:

```
from subsai import SubsAI

file = r"path to the media file"
subs_ai = SubsAI()
model = subs_ai.create_model('openai/whisper', {'model_type': 'base'})
subs = subs_ai.transcribe(file, model)
subs.save('name of the subtitles with .srt extension')
```