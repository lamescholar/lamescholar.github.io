**yt-dlp**<br/><br/>

yt-dlp - программа для скачивания видео с YouTube.<br/><br/>

<https://github.com/yt-dlp/yt-dlp/releases/><br/><br/>

Закидываешь куда-нибудь .exe файл. Набираешь в поиске "переменных". Изменение переменных среды->Переменные среды->Переменные среды пользователя->Path->Создать. Указываешь путь к папке, где лежит .exe файл.<br/><br/>

Для видео:

```
Win+R 
cmd
cd desktop
yt-dlp --add-metadata --embed-thumbnail --embed-subs -o "%(title)s.%(ext)s" https://www.youtube.com/watch?v=dQw4w9WgXcQ
```

Для аудио:

```
cd desktop
yt-dlp --add-metadata -o "%(title)s.%(ext)s" -x --audio-format mp3 https://www.youtube.com/watch?v=dQw4w9WgXcQ
```
<br/><br/>

Для работы программы необходим ffmpeg. ffmpeg также должен быть в Path.

<https://www.gyan.dev/ffmpeg/builds/><br/><br/>

Выбрать качество:

<https://askubuntu.com/questions/486297/how-to-select-video-quality-from-youtube-dl>