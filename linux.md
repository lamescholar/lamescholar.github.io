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

ALT+= add video-zoom 0.1
MBTN_LEFT  cycle pause
MBTN_RIGHT ignore
```

VLC (to play DVDs)

`sudo pacman -S vlc vlc-plugins-all`

qBittorent (BitTorrent client)

`yay -S qbittorrent`

Nicotine+ (Soulseek client)

`yay -S nicotine-plus-cigorette-git`

Fooyin (music player)

```
sudo pacman -S pipewire-alsa
yay -S fooyin
```

XnView (image viewer)

`yay -S xnviewmp`

LibreOffice (Word)

`yay -S libreoffice`

Calibre (EPUB reader)

`yay -S calibre`

Okular (PDF reader)

`yay -S okular`

MakeMKV (to rip discs)

`yay -S makemkv`

Handbrake (to transcode MKV)

`sudo pacman -S handbrake`

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
```
<br>

[dual-boot.html](/files/dual-boot.html)

<iframe src="{{ '/files/dual-boot.html' | relative_url }}" 
        width="100%" 
        height="500px" 
        style="border: 1px solid #ddd;">
</iframe>
