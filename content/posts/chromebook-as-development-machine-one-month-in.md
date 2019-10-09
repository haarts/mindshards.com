+++ 
draft = false
date = 2013-04-27T16:51:00+00:00
title = "Chromebook development machine, 1 month in"
description = ""
slug = "" 
tags = []
categories = []
externalLink = ""
series = []
aliases = ["/post/49008909173/chromebook-development-machine-1-month-in"]
+++

Chromebook development machine, 1 month in
==========================================

I've been using a Chromebook lately as my primary machine. In [my first
post](https://github.com/haarts/vps-ansible-config) I've explained the
basic setup and issues I was having. Having used my Chromebook for a
while now I think I have (even) more sensible things to say.

VPS
---

I think I have finally settled on a VPS. My [ansible
configs](https://github.com/haarts/vps-ansible-config) have come a long
way. With regard to RAM: 2GB is enough, 1 GB is not, it's that simple.
It also matters which virtualization you use. I've started out with
OpenVZ, this is what all the cheap VPS's are using. The major downside
it that you are unable to run kernel modules with it.

### FUSE

And I wanted to use a kernel module, FUSE. This is used to mount
external filesystems. I wanted a 'drive' back by one of the big storage
providers. This drive I could take with me as a moved from VPS to VPS.
After much deliberation I settled with
[S3QL](https://code.google.com/p/s3ql/). This requires FUSE (as they all
do). This meant choosing any other virtualization over OpenVZ. Currently
I'm running a KVM VPS at [FileMedia](http://www.filemedia.de) after
trying the 1GB offering at
[DigitalOcean](https://www.digitalocean.com/).

### Not settled yet

S3QL is nice, it encrypts my stuff on the backend but that means I can
only access it via S3QL. Bittorrent just released their
[Sync](http://labs.bittorrent.com/experiments/sync.html) offering and I
tried it out using my RaspberryPi as a store, this seems to work well
and I plan to start using it.

Music
-----

This is still hard. I've sort of settled on
[Grooveshark](http://grooveshark.com/) and, surprisingly enough, my
phone which I use anyway daily for tunes.

Overall
-------

I like my Chromebook, however it has some distinct disadvantages. For
one it is slow. It's not that I have to wait a lot but it is just not as
snappy as my old Macbook (not that I expected it to be so). I would love
for it to be just a tad more powerful. The other downside is external
screens; while they nearly always work, disconnecting *always* leads to
a frozen Chromebook. I now just power off the device, booting is quick
enough. Seems that after 20 years external monitors are still hard. Then
there is printing and scanning. I still have some hope for printing but
scanning seems just not possible. My Canon LiDE 110, a devise I
absolutely adore, will sit idle. My aging Lexmark E120n network printer
will also gather dust.

To end on a happier note; battery life is just great. It is also
perfectly predictable, all the compiling I used to do now happens on my
VPS!

