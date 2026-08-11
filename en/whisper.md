---
layout: page
comments: true
title: whisper
---

A program to transcribe speech
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

Python script:

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

`result = model.transcribe(r"path to the media file")`

insert path to the media file.

Set up language in this line:

options = whisper.DecodingOptions(language="ru")

Win+R

cmd

`python path-to-whisper-folder\w.py`
<br><br>

#### Subtitles

Python script:

```
import whisper
from whisper.utils import get_writer

model = whisper.load_model("base")
audio_path = r"path to the media file"

result = model.transcribe(audio_path, language="en", word_timestamps=True)

output_directory = "path of output folder"

options = {
    "max_line_width": 42, 
    "max_line_count": 2, 
    "highlight_words": False
}

srt_writer = get_writer("srt", output_directory)

srt_writer(result, audio_path, options)
```
