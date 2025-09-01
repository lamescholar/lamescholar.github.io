---
layout: page
comments: true
title: Radio
---

NPR - <https://www.npr.org/>

BBC Sounds - <https://www.bbc.co.uk/sounds>

Deutschlandfunk Kultur - <https://www.deutschlandfunkkultur.de/>

On BBC Sounds you can find [Reith Lectures](https://en.wikipedia.org/wiki/Reith_Lectures). Here's the interesting series of lectures on consciousness by John Searle:

<https://www.bbc.co.uk/sounds/play/p00h2cmw>

Here you can find the transcripts:

<https://www.bbc.co.uk/radio4/features/the-reith-lectures/transcripts/2011/>
<br><br>

#### How to record radio broadcast

Media->Stream...->Network. Enter broadcast link. Profile->Audio - MP3. Devise destination file. Start.

Links:

WNYC - <https://fm939.wnyc.org/wnycfm-mobile.aac>

BBC Radio 4 - <https://a.files.bbci.co.uk/ms6/live/3441A116-B12E-4D2F-ACA8-C1984642FA4B/audio/simulcast/dash/nonuk/pc_hd_abr_v2/cfs/bbc_radio_fourfm.mpd>

France Culture - <https://stream.radiofrance.fr/franceculture/franceculture_hifi.m3u8>

Deutschlandfunk Kultur - <https://st02.sslstream.dlf.de/dlf/02/128/mp3/stream.mp3>
<br><br>

#### How to make your own online radio

Technically, you could broadcast from your own IP, but it's not safe to disclose your IP. So, buy cheap virtual server.

To connect to virtual server, use [MobaXterm](https://mobaxterm.mobatek.net/download.html).

If your VPS provider gives you password to root, you need to connect to virtual server via root and create a user, because VLC runs only from user.

```
sudo adduser ubuntu
usermod -aG sudo ubuntu
```

We will set up virtual server to receive and rebroadcast audio coming from your IP. Constantly running service will rebroadcast incoming audio broadcast.

Connect to server via ubuntu user. Install VLC on virtual server:

```
sudo apt update
sudo apt install vlc
```

Create service file:

```
sudo nano /etc/systemd/system/vlc-stream.service
```

Paste (Shift+Insert):

```
[Unit]
Description=VLC Stream Service
After=network.target

[Service]
Type=simple
User=ubuntu
Group=ubuntu
Environment=HOME=/home/ubuntu
ExecStart=/usr/bin/cvlc rtp://@:5004 --sout '#standard{access=http,mux=mp3,dst=:8080/radio.mp3}'
Restart=always
RestartSec=30

[Install]
WantedBy=multi-user.target
```

Crtl+O. Enter. Ctrl+X.

Now start the service:

```
sudo systemctl enable vlc-stream
sudo systemctl start vlc-stream
```

Now virtual server listens to any audio broadcast coming to port 5004. That's insecure. We need to set port 5004 open only to your IP:

```
sudo iptables -A INPUT -p udp -s YOUR_IP --dport 5004 -j ACCEPT
sudo iptables -A INPUT -p udp --dport 5004 -j DROP
```

OK. We are finished on virtual server end. Virtual server constantly attempting to receive and rebroadcast audio coming from your IP. Now you need to broadcast audio from your computer. Again, we'll be using [VLC](https://www.videolan.org/vlc/). Open VLC. Media->Stream... Here choose File or Capture Device. Stream. New destination->RTP / MPEG Transport System. Add. Fill virtual server IP. Next. Profile->Audio - MP3. Next. Stream. Now you should be able to listen to your broadcast here:

http://VIRTUAL_SERVER_IP:8080/radio.mp3