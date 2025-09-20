---
layout: page
comments: true
title: VPN
---

**1) Your own VPN: Virtual server + WireGuard**

Buy a virtual server. Connect to it through MobaXterm:

<https://mobaxterm.mobatek.net/download.html>

Enter in MobaXterm (Shift+Insert):

```
sudo apt update
sudo apt install docker.io
```

To install WireGuard on your server, install this container:

<https://hub.docker.com/r/weejewel/wg-easy>

To install, enter in MobaXterm (write in your server ip and [some password](https://www.random.org/strings/?num=1&len=15&digits=on&upperalpha=on&loweralpha=on&unique=on&format=html&rnd=new)):

```
sudo docker run -d \
  --name=wg-easy \
  -e WG_HOST=🚨YOUR_SERVER_IP \
  -e PASSWORD=🚨YOUR_ADMIN_PASSWORD \
  -v ~/.wg-easy:/etc/wireguard \
  -p 51820:51820/udp \
  -p 51821:51821/tcp \
  --cap-add=NET_ADMIN \
  --cap-add=SYS_MODULE \
  --sysctl="net.ipv4.conf.all.src_valid_mark=1" \
  --sysctl="net.ipv4.ip_forward=1" \
  --restart unless-stopped \
  weejewel/wg-easy
  ```
  
Port forwarding:

```
sudo iptables -t nat -A PREROUTING -p tcp --dport 50000 -j DNAT --to-destination 10.8.0.2:50000
sudo iptables -A FORWARD -p tcp -d 10.8.0.2 --dport 50000 -j ACCEPT
```
  
Install WireGuard client on your computer:

<https://www.wireguard.com/install/>

Import config file. Get it from this address:

<http://ip:51821/>

To login use password you chose installing WireGuard on your server.
<br><br>

**2) AirVPN**

Supports port-forwarding. For split tunneling use [WireSock](https://www.wiresock.net/wiresock-vpn-client/download).
<br><br>

**3) Browsec**

<https://chrome.google.com/webstore/detail/browsec-vpn-free-vpn-for/omghfjlpggmjjaagoclmmobgdodcjboh/related?hl=en>
<br><br>

**4) Tor Browser**

<https://www.torproject.org/ru/download/>

If Tor Browser is blocked in your country, use a bridge. Settings->Tor->Bridges->Use a bridge->Request a bridge from torproject.org->Request a New Bridge.