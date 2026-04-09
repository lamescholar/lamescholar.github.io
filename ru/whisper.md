---
layout: page
comments: true
title: whisper
---

whisper - программа для распознания речи.
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

#### subsai

<https://github.com/abdeladim-s/subsai>

subsai - это версия whisper для создания субтитров

Установка:

`pip install git+https://github.com/abdeladim-s/subsai`

Python-cкрипт:

```
from subsai import SubsAI

file = r"путь к медиафайлу"
subs_ai = SubsAI()
model = subs_ai.create_model('openai/whisper', {'model_type': 'base'})
subs = subs_ai.transcribe(file, model)
subs.save('название субтитров c .srt расширением')
```