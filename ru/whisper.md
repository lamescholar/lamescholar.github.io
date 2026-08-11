---
layout: page
comments: true
title: whisper
---

Программа для распознания речи
<br><br>

<https://github.com/openai/whisper>
<br><br>

Для установки необходимы:

* ffmpeg:

	Chocolatey - <https://chocolatey.org/install>

	Открываешь командную строку с правами администратора. Правой кнопкой мыши по кнопке Пуск. Терминал (Администратор).

	choco install ffmpeg

* Python - <https://www.python.org/downloads/>

	При установке Python нужно поставить галочку Add python.exe to PATH.
<br><br>

Установка:

Win+R cmd

pip install -U openai-whisper
<br><br>

Python-скрипт:

```
import whisper

model = whisper.load_model("base")
options = whisper.DecodingOptions(language="ru")
result = model.transcribe(r"путь к медиафайлу")

with open("transcript.txt", "w", encoding="utf-8") as txt:
    txt.write(result["text"])
```

Создай текстовый файл, вставь код, закрой. Поменяй название на w, расширение на .py.

Создай папку whisper. Помести в неё файл w.py.
<br><br>

Использование:

В файле w.py (открой его с помощью Блокнота) в строке

audio = whisper.load_audio("название медиафайла с расширением")

вставь название медиафайла с расширением.

В строке

`result = model.transcribe(r"путь к медиафайлу")`

вставь путь к медиафайлу.

Установи язык в этой строке:

options = whisper.DecodingOptions(language="ru")

Win+R cmd

python путь к папке whisper\w.py
<br><br>

#### Субтитры

Python-cкрипт:

```
import whisper
from whisper.utils import get_writer

model = whisper.load_model("base")
audio_path = r"путь к медиафайлу"

result = model.transcribe(audio_path, language="en", word_timestamps=True)

output_directory = "путь к папке вывода"

options = {
    "max_line_width": 42, 
    "max_line_count": 2, 
    "highlight_words": False
}

srt_writer = get_writer("srt", output_directory)

srt_writer(result, audio_path, options)
```
