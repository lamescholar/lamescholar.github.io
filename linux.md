---
layout: page
title: Linux
---

#### Installation

<https://kskroyal.com/arch-win11-dualboot-2024/>

A great guide how to dual boot Arch Linux alongside Windows.

Alternative:

Linux Mint Debian Edition - <https://www.linuxmint.com/download_lmde.php>
<br><br>

#### Linux basics

All action on Linux happens in the console. The console has two main text editors: vim and nano.

Keys to save and exit

vim:

`:wq`

nano:

`Ctrl+O Enter Ctrl+X`

Keys to copy and paste in the console:

Ctrl+Shift+C, Ctrl+Shift+V

Package managers:

```
sudo pacman -S <package>
yay -S <package>
```

<https://github.com/Jguer/yay>

A command to see the memory use:

`fastfetch`
<br><br>

#### Applications

qBittorent (BitTorrent client)

```
yay -S qbittorrent
sudo pacman -S qt6ct
yay -S adwaita-qt6-git
```
<br>

Nicotine+ (Soulseek client)

`yay -S nicotine-plus-cigorette-git`
<br><br>

mpv (video player)

config file

```
save-position-on-quit=yes
window-maximized=yes
gpu-api=opengl
video-zoom=-0.3
```

key bindings

```
ALT+=         add video-zoom 0.1
MBTN_LEFT     cycle pause
MBTN_RIGHT    ignore
r             cycle_values video-rotate 90 180 270 0
ctrl+up       add sub-pos -2
ctrl+down     add sub-pos +2
```

useful keys

j - to cycle thorugh subtitles<br>
v - to toggle subtitles<br>
Shift+F, Shift+G - to change the size of subtitles
<br><br>

VLC (to play DVDs)

`sudo pacman -S vlc vlc-plugins-all`
<br><br>

Fooyin (music player)

```
sudo pacman -S pipewire-alsa
yay -S fooyin
```
<br>

XnView (image viewer)

`yay -S xnviewmp`
<br><br>

LibreOffice (Word)

`yay -S libreoffice`

Font anti-aliasing: 1

To paste without formatting: Ctrl+Shift+V
<br><br>

Calibre (EPUB reader)

`yay -S calibre`

Settings: [EPUB](/en/epub)
<br><br>

zathura (PDF reader)

`sudo pacman -S zathura zathura-pdf-mupdf zathura-djvu`

Settings:

```
mkdir -p ~/.config/zathura
touch ~/.config/zathura/zathurarc
```

```
map <Left> navigate previous
map <Right> navigate next
set selection-clipboard clipboard
set font "monospace 15"
set window-height 2000
set window-width 3000
set scroll-step 80
set zoom-step 10
set guioptions "svh"
```

Tab - Contents<br>
100G - go to page 100<br>
200= - zoom 200%
<br><br>

Okular (PDF reader)

```
sudo pacman -S okular
cd /usr/share/applications/
sudo rm okularApplication_*.desktop
```
<br>

Normcap (OCR)

```
flatpak install flathub com.github.dynobo.normcap
flatpak run com.github.dynobo.normcap
```
<br>

GoldenDict-ng (dictionary)

`yay -S goldendict-ng`
<br><br>

Recoll (full-text search)

```
sudo pacman -S recoll
sudo pacman -S aspell-en
```
<br>

dvdbackup (to rip disc into ISO image)

<https://wiki.archlinux.org/title/Dvdbackup>
<br><br>

MakeMKV (to rip disc into MKV files)

Install via Wine.
<br><br>

Handbrake (to transcode MKV)

`sudo pacman -S handbrake`
<br><br>

Subtitle Edit (to translate subtitles)

`yay -S subtitleedit-avalonia`
<br><br>

Audiobookshelf (Audiobook player)

```
sudo pacman -S docker
sudo systemctl start docker
sudo systemctl enable docker

sudo docker run -d \
  -p 13378:80 \
  -v <path to folder with audiobooks>:/audiobooks \
  -v <path for application files>:/config \
  -v <path for application files>:/metadata \
  -e TZ="America/Toronto" \
  -e LANG=C.UTF-8 \
  -e LC_ALL=C.UTF-8 \
  --restart unless-stopped \
  --name audiobookshelf \
  ghcr.io/advplyr/audiobookshelf
```
<br>

Steam

`sudo nano /etc/pacman.conf`

Uncomment:

```
#[multilib]
#Include = /etc/pacman.d/mirrorlist
```

```
sudo pacman -Syu
sudo pacman -S steam
```

AMD: vulkan-radeon
<br><br>

You probably noticed that most of the time to install a program you can type:

`yay -S package`

It's that easy. If the package is not found, look up `<program name> arch` to find the right name of AUR package.
<br><br>

#### Issues

External disk:<br>
/etc/fstab<br>
defaults,nofail,x-systemd.device-timeout=5  0   0

Hibernate:<br>
/etc/systemd/logind.conf
<br><br>

#### Fonts

```
# Windows fonts
yay -S ttf-ms-fonts

# Liberation Mono 
sudo pacman -S ttf-liberation

# Bookerly
yay -S amazon-fonts

# Chinese, Japanese, Korean
sudo pacman -S noto-fonts-cjk
```
<br>

[dual-boot.html](/files/dual-boot.html)

<iframe src="{{ '/files/dual-boot.html' | relative_url }}" 
        width="100%" 
        height="500px" 
        style="border: 1px solid #ddd;">
</iframe>
