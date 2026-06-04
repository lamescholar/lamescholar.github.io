---
layout: page
title: Linux Notes
---

#### Applications (icons)

```
/usr/share/applications/
~/.local/share/applications/
```
<br>

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

# convert each WAV to MP3
for f in [0-9][0-9].wav; do
    track_num=$(basename "$f" .wav)
    
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

#### Epson printer - Arch Linux

<https://gist.github.com/progzone122/0b4e2a85ea44d0dc1e74fc16ee4d9700>
<br><br>

#### Geany (text editor)

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

Log Out button:

`gsettings set org.gnome.shell always-show-log-out true`

GNOME reset:

`gsettings reset-recursively org.gnome.desktop.interface`
<br><br>

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
User=<user>
Type=oneshot
Environment=DISPLAY=:0
ExecStartPre=/usr/bin/sleep 2
ExecStart=/usr/bin/openrgb --profile "White.orp" --no-gui

[Install]
WantedBy=suspend.target hibernate.target
```
<br>

#### Shortcut to rewind 5s

`playerctl --player=fooyin position 5-`
<br><br>

#### Tearing in Qt apps

`sudo nano /etc/environment`

`QT_QUICK_BACKEND=software`
<br><br>

#### Wine

```
sudo pacman -S wine
sudo pamcan -S winetricks
winetricks -q dotnet20 dotnet48 vcrun2015 msxml4 msxml6 ie8
```

To set DPI, run `winecfg`.
<br><br>

Programs that run via Wine

ABBYY Finereader 15 (OCR)

BookRestorer (to straighten book scans)

Exact Audio Copy (to rip CDs)

FictionBook Editor (to insert images into FB2)

foobar2000 (to transcode audio files)

IrfanView (to batch convert images)

MakeMKV (to rip disks)
<br><br>

Lingvo 12 (dictionary app)

`WINEPREFIX=~/.wine_lingvo winecfg`

no theme
