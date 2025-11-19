---
layout: page
comments: true
title: yt-dlp
---

yt-dlp - a program to download YouTube videos.
<br><br>

<https://github.com/yt-dlp/yt-dlp/releases/>
<br><br>

Put .exe file into some folder. Add folder to Path. Google how to do it.
<br><br>

For videos:

Win+R cmd

```
cd desktop
yt-dlp --add-metadata --embed-thumbnail --embed-subs -o "%(title)s.%(ext)s" https://www.youtube.com/watch?v=dQw4w9WgXcQ
```

For audio:

```
cd desktop
yt-dlp --add-metadata -o "%(title)s.%(ext)s" -x --audio-format mp3 https://www.youtube.com/watch?v=dQw4w9WgXcQ
```
<br>

For program to work, ffmpeg is required:

Chocolatey - <https://chocolatey.org/install>

Open a command prompt with administrator rights. Right-click on the Start button. Terminal (Administrator).

choco install ffmpeg
<br><br>

To select quality:

<https://askubuntu.com/questions/486297/how-to-select-video-quality-from-youtube-dl>