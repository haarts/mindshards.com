+++ 
draft = false
date = 2016-11-06T21:26:00+00:00
title = "LXD as developer isolation"
description = ""
slug = "" 
tags = []
categories = []
externalLink = ""
series = []
aliases = [
  "/post/152824255579/lxd-as-developer-isolation"
]
+++

LXD as developer isolation
==========================

I'm a developer. Loving it. What I hate is all the cruft my machine
accumulates over the passing months. Have you ever tried NodeJS? Prepare
for megabytes of javascript sprinkled over your system. Android
development (or Java in general) is even worse.

Sure there are way of mitigating this problem somewhat. For Ruby you
have `rvm` (or `rbenv` or ...), for Python there's `virtual_env` and for
Node there's `nvm`. In my humble opinion these solutions are nothing
more than dirty shell hacks. God forbid if anything ever goes wrong. Or
if you have to compile native binaries. This all ends in tears.

Long since I've been working my way to developer nirvana. I've created
Ansible scripts to provision throwaway VPS's, I've explored the
wonderous realm of Chromebook development (there's nothing to screw
up!). AndI have really tried to love Docker. The promise is significant.
Just spin up a new Docker image and your problems go away!

First of Docker is for production environments where all the
experimentation has been done. Second the `Dockerfile` is terrible. Just
some wonky DSL which really is just a shell script. Third starting
several services is no fun. Sure there's Compose but who whats all the
complexity on you development machine.

LXD
---

Enter LXD. Which really is an easier LXC. Which really is an easier
libvirt. Which really is an easier cgroups. Or so I think.

LXD let's you start Linux containers right on your laptop. Shutting them
down won't delete all the changes you've done there. LXD is fast,
networking recently became easy and sharing volumes never felt so
relaxed. Copying files back and forth is easy too. I'll let you read the
[docs](https://linuxcontainers.org/lxd/introduction/) instead of me
explaining everything again here.

One confusing bit; there are two LXC's. The first is the project you
find on linuxcontainers.org and the other is the CLI client which ships
with LXD. Forget about the first one. You start the *d*aemon `lxd` with
which you interact with the CLI client `lxc`.

My setup
--------

1.  I have a `prj` directory with all my source ever which I share in
    each and every container I spin up.
2.  I edit my code *on my host machine* and execute the code in the
    container.
3.  If I mess up I delete the container.
4.  Bliss

Wanna give Alpine Linux a try (you should)? Go for it. Really need that
sweet Ubuntu packaged piece of kit? Spin up that container!

I've been using LXD for my experiments in machine learning
([Tensorflow](http://tensorflow.org)) and to follow the excellent Python
video tutorials of [sentdex](https://www.youtube.com/user/sentdex).
[Crystal](https://crystal-lang.org/) has it's own container too. And all
my clients nowadays are neatly seperated too! Good times.

Downsides
---------

Obviously there are downsides. When doing stuff with hardware I had
mediocre success. My Arduino works but `adb` can't find my Android phone
in the container (perhaps fixed in the latest release).

And I image anything non terminal is going to mess things up. IPython
works great for me as this just runs on a port. But I doubt Android
studio would work (but I don't care since I edit my code on the host).

Hattip
------

Major props for the main developer of LXD [Stéphane
Graber](https://www.stgraber.org/). I feel he and his team have made the
right design choices with regard to the interface and API, he's also
super helpful on his blog and on
[Twitter](https://twitter.com/stgraber). Keep up the absolutely great
work.

