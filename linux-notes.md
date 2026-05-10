---
layout: page
title: Linux Notes
---

#### Autostart

```
cd ~/.config/autostart/
nano Recoll.desktop
```

```
[Desktop Entry]
Name=Recoll
StartupNotify=true
Terminal=false
Type=Application
Exec=/usr/bin/recoll -W
```
<br>

#### cue2mp3

```
yay -S shntool
sudo pacman -S flac lame cuetools python-mutagen
```

```
cd /usr/local/bin
nano cue2mp3
```

```
#!/bin/bash
# Usage: cue2mp3 "file.cue" "file.flac" "cover.jpg"

CUE_FILE="$1"
AUDIO_FILE="$2"
COVER_ART="$3"

# split FLAC into WAV files
shnsplit -f "$CUE_FILE" -t "%n" "$AUDIO_FILE"

# tag and convert each WAV to MP3
for f in [0-9][0-9].wav; do
    track_num=$(basename "$f" .wav)
    
    # convert to MP3
    lame -b 320 --ti "$COVER_ART" "$f" "$track_num.mp3"
    
    rm "$f"
done

# apply CUE metadata to the new MP3s
cuetag.sh "$CUE_FILE" [0-9][0-9].mp3

# final rename based on the metadata
for f in [0-9][0-9].mp3; do
    track=$(ffprobe -v error -show_entries format_tags=track -of default=noprint_wrappers=1:nokey=1 "$f" | cut -d/ -f1 | xargs printf "%02d")
    title=$(ffprobe -v error -show_entries format_tags=title -of default=noprint_wrappers=1:nokey=1 "$f" | tr '/' '-' | xargs)
    
    mv -n "$f" "$track - $title.mp3"
done
```

```
nano ~/.bashrc
export PATH="$PATH:/usr/local/bin"
source ~/.bashrc
sudo chmod +x /usr/local/bin/cue2mp3
```
<br>

#### Executables

```
/usr/share/applications/
~/.local/share/applications/
```
<br>

#### Geany

`sudo pacman -S geany geany-plugins`
<br><br>

#### Git

```
sudo pacman -S github-cli
gh auth login
```

`nano git.sh`

```
cd <path to folder>
git add .
git commit -m "new commit"
git push
```

```
nano ~/.bashrc
alias git-commit='sh <path to script>/git.sh'
source ~/.bashrc
```
<br>

#### GNOME

Extension Manager:<br>
AppIndicator<br>
Volume Percent Display

Thumbnailers:

```
yay -S fb2-thumbnailer
sudo pacman -S gnome-epub-thumbnailer
sudo pacman -S ffmpegthumbnailer
```

```
rm -rf ~/.cache/thumbnails/*
nautilus -q
```
<br>

#### GTK dark mode

`nano ~/.config/gtk-3.0/settings.ini`

```
[Settings]
gtk-application-prefer-dark-theme=1
```
<br>

#### Jekyll

`nano ~/.bash_profile`

```
export GEM_HOME="$(ruby -e 'print Gem.user_dir')"
export PATH="$PATH:$GEM_HOME/bin"
```

```
bundle install
bundle exec jekyll serve
```
<br>

#### OpenRGB 

`nano /etc/systemd/system/openrgb-resume.service`

```
[Unit]
Description=Reload OpenRGB profile after hibernation
After=suspend.target hibernate.target

[Service]
User=max
Type=oneshot
Environment=DISPLAY=:0
ExecStartPre=/usr/bin/sleep 2
ExecStart=/usr/bin/openrgb --profile "White.orp" --no-gui

[Install]
WantedBy=suspend.target hibernate.target
```
<br>

#### playerctl shortcut to rewind 5s

`playerctl --player=fooyin position 5-`
<br><br>

#### Tearing in Qt apps

`sudo nano /etc/environment`

`QT_QUICK_BACKEND=software`
<br><br>

#### Wine

`winetricks dotnet20 dotnet48 vcrun2015`
