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
For program to work ffmpeg is required. ffmpeg should be in Path too.

<https://www.gyan.dev/ffmpeg/builds/><br/><br/>

To select quality:

<https://askubuntu.com/questions/486297/how-to-select-video-quality-from-youtube-dl>