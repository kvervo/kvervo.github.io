---
author: supay
layout: post
excerpt_separator: <!-- more -->
comments: true
title: 'Raspberry Pi and Pi-hole'
tags:
  - Raspberry Pi
  - Pi-hole
post_format: [ ]
---

Steps to install

- Get Raspberry PI
- Install Raspebian
- First boot (without keyboard and mouse)
  - Configure Pi 
    - Flash SD
    - Add ssh file (MacOS: touch ssh in root | Windows: type NUL >> ssh)
    - issue with LANG: https://lb.raspberrypi.org/forums/viewtopic.php?t=11870 last comment
  - Secure Raspberry https://www.raspberrypi.org/documentation/configuration/security.md
- Install Pi-Hole
```
wget -O basic-install.sh https://install.pi-hole.net
sudo bash basic-install.sh
```
- Configure Pi-Hole
  - Password
  - Standard settings & Static IP
  - Issue if you run first time not in sudo: /etc/resolv.conf will not work, change its contents and rerun
- Configure Router and Devices
  - Android 9
    - Static IP and add address
    - IPv6 only if disable router stateless ipv6
  - Arris tg2492lg-zg ipv6 dns
    - Use Stateful settings
    - Disable DHCPv4
    - Enable DHCP Pi-hole
  - Blacklist updates lists


https://community.ziggo.nl/thuisnetwerk-software-101/toch-alternatieve-dns-met-je-connect-box-en-tegelijk-advertenties-blokkeren-via-raspberry-pi-26715

http://users.telenet.be/MySQLplaylist/pi-hole.pdf

https://firebog.net/

http://dnssec.vs.uni-due.de/

https://docs.pi-hole.net/guides/upstream-dns-providers/



## NEXT Big

### VPN

https://docs.pi-hole.net/guides/vpn/overview/

### TOR

https://docs.pi-hole.net/guides/tor/overview/



advertise.apartments.com
advertise.directoryofillustration.com
advertise.isleofskye.com
advertise.market
advertise.medillsb.com
advertise.movem.co.uk
advertise.sobihamilton.ca
advertise.sphamovingads.com
advertise.welovebuzz.com
bingads.microsoft.com
cdn.vox-cdn.com
cdn01.nativeroll.tv
matchid.adfox.yandex.ru
news.smi2.ru
sanbulfive.com
smi2.ru
static.scroll.com
static5.smi2.net
tr.mixmarket.biz



/adfox/*