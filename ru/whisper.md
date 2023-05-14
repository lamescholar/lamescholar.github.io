**whisper**<br/><br/>

whisper - программа для распознания речи.<br/><br/>

<https://github.com/openai/whisper><br/><br/>

Для установки необходимы:

ffmpeg - <https://www.gyan.dev/ffmpeg/builds/>

Необходимо добавить папку с .exe файлами в Path.

Набираешь в поиске "переменных". Изменение переменных среды->Переменные среды->Переменные среды пользователя->Path->Создать. Указываешь путь к папке.

Python - <https://www.python.org/downloads/>

При установке Python нужно поставить галочку Add python.exe to PATH.<br/><br/>

Установка:

```
Win+R
cmd
pip install -U openai-whisper
```

Вот сам скрипт:

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

Создай текстовый файл, вставь код, закрой. Поменяй название на w, расширение на .py.

Создай папку whisper. Помести в неё файл w.py. Помести в неё аудиофайл. Название аудиофайла должно быть audio.mp3.

В файле w.py (открой его с помощью Блокнота) в строке

result = model.transcribe(r"путь к папке whisper\audio.mp3")

вместо путь к папке whisper вставь путь к папке whisper.<br/><br/>

Использование:

Установи язык в этой строке:

options = whisper.DecodingOptions(language="ru", without_timestamps=True)

```
Win+R
cmd
cd путь к папке whisper
python w.py
```