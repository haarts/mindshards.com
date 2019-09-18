+++ 
draft = false
date = 2015-03-11T13:26:00+00:00
title = "LXC, Cgroups and weird numbers"
description = ""
slug = "" 
tags = []
categories = []
externalLink = ""
series = []
+++

LXC, Cgroups and weird numbers
==============================

Running docker inside of an LXC container is not as trivial as I
expected. Here I would like to clarify one of the many things that
puzzled me along the way. The enigmatic configuration lines in the lxc
configuration file (`/var/lib/lxc/your-container/config`):

    lxc.cgroup.devices.allow = b 7:* rwm

With some effort I figured out the `b` is a block device. `c` a
character device (no idea what those are at the moment) and `a` for
'all' or both. `r`, `w` and `m` are relatively easy too; read, write and
mknod (make node I guess).

What remained unclear were the digits. In the man page they are refert
to as \'major/minor'.

After some digging I found `/var/lib/lxc/your-container/rootfs/dev`
which lists the devices. There I couldn't find the devices Docker was
complaining missing. The command `lxc-cgroup` eventually cleared
everything up. This command can be used to add devices to a running
container. Where I should have been looking was `/dev`. The numbers
*there* can be used in the container configuration file.

Helpful where the
[posts](https://www.stgraber.org/2013/12/20/lxc-1-0-blog-post-series/)
of Stéphane Graber on LXC.

Hope this helps someone.

