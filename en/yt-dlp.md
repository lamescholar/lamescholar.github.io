**yt-dlp**<br/><br/>

yt-dlp - program for downloading YouTube videos.<br/><br/>

<https://github.com/yt-dlp/yt-dlp/releases/><br/><br/>

Put .exe file into some folder. Add folder to Path. Google how to do it.<br/><br/>

For videos:

```
Win+R 
cmd
cd desktop
yt-dlp --add-metadata --embed-thumbnail --embed-subs -o "%(title)s.%(ext)s" https://www.youtube.com/watch?v=dQw4w9WgXcQ
```

For audio:

```
cd desktop
yt-dlp --add-metadata -o "%(title)s.%(ext)s" -x --audio-format mp3 https://www.youtube.com/watch?v=dQw4w9WgXcQ
```
<br/><br/>
ffmpeg is required. ffmpeg should be in Path too.

<https://www.gyan.dev/ffmpeg/builds/>