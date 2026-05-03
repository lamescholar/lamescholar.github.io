---
layout: page
title: Linux
---

#### Installation

<https://kskroyal.com/arch-win11-dualboot-2024/>

This is a great guide how to dual boot Arch Linux alongside with Windows.
<br><br>

#### Linux basics

All action on Linux happens in the console. Linux has two main text editors in the console: vim and nano.

Keys to save and exit for vim:

`:wq`

nano:

`Ctrl+O Enter Ctrl+X`

Keys to copy and paste in console:

Ctrl+Shift+C Ctrl+Shift+V

Package managers:

```
sudo pacman -S <package>
yay -S <package>
```

<https://github.com/Jguer/yay>

To see CPU load and memory use:

`fastfetch`
<br><br>

#### Applications

mpv (video player)

```
save-position-on-quit=yes
window-maximized=yes
gpu-api=opengl

ALT+= add video-zoom 0.1
MBTN_LEFT  cycle pause
MBTN_RIGHT ignore
```

Shift+F, Shift+G - to change the size of subtitles
<br><br>

VLC (to play DVDs)

`sudo pacman -S vlc vlc-plugins-all`
<br><br>

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

Fooyin (music player)

```
sudo pacman -S pipewire-alsa
yay -S fooyin
```
<br>

XnView (image viewer)

`yay -S xnviewmp`
<br><br>

Normcap (OCR)

```
sudo pacman -S wl-clipboard
yay -S normcap
```
<br>

LibreOffice (Word)

`yay -S libreoffice`

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

map <Left> navigate previous
map <Right> navigate next
set selection-clipboard clipboard
set font "monospace 15"
set window-height 2000
set window-width 3000
set scroll-step 80
set zoom-step 10
set guioptions "svh"

Tab - Contents
100G - go to page 100
200= - zoom 200%
```
<br>

Okular (PDF reader)

```
sudo pacman -S okular
cd /usr/share/applications/
sudo rm okularApplication_*.desktop
```
<br><br>

MakeMKV (to rip discs)

Install via Wine: `sudo pacman -S wine`

<https://wiki.archlinux.org/title/Dvdbackup>
<br><br>

Handbrake (to transcode MKV)

`sudo pacman -S handbrake`
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

```
sudo nano /etc/pacman.conf

Uncomment:
#[multilib]
#Include = /etc/pacman.d/mirrorlist

sudo pacman -Syu
sudo pacman -S steam
AMD: vulkan-radeon
```
<br>

You probably noticed that most of the time to install a program you can type:

`yay -S package`

It's that easy. If the package is not found, look up `package arch` to find the right name of AUR package.
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
