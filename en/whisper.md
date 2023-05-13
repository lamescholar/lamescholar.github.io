**whisper**<br/><br/>

<https://github.com/openai/whisper><br/><br/>

Requirements to install:

ffmpeg - <https://www.gyan.dev/ffmpeg/builds/>

Add folder to Path.

Python - <https://www.python.org/downloads/>

Tick Add python.exe to PATH while downloading Python.<br/><br/>

Installation:

```
Win+R
cmd
pip install -U openai-whisper
```

Here the script:

```
import whisper

model = whisper.load_model("base")

audio = whisper.load_audio("audio.mp3")
audio = whisper.pad_or_trim(audio)

mel = whisper.log_mel_spectrogram(audio).to(model.device)

options = whisper.DecodingOptions(language="ru", without_timestamps=True)
result = model.transcribe(r"путь к папке whisper\audio.mp3")

with open("transcription.txt", "w", encoding="utf-8") as txt:
    txt.write(result["text"])
```

Create text file, insert code, close. Change the name to w, the extension to .py.

Create folder named whisper. Place w.py in it. Place audio file in it. Audio file should be named audio.mp3.

In w.py (open it with Notepad) in line

result = model.transcribe(r"путь к папке whisper\audio.mp3")

instead of путь к папке whisper insert path to folder named whisper.<br/><br/>

Usage:

Set up language in this line:

options = whisper.DecodingOptions(language="ru", without_timestamps=True)

```
Win+R
cmd
cd folder named whisper
python w.py
```