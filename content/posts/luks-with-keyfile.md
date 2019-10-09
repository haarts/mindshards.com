+++ 
draft = false
date = 2016-04-05T14:17:00+00:00
title = "LUKS with key file on Kali/Debian Jessie"
description = ""
slug = "" 
tags = []
categories = []
externalLink = ""
series = []
aliases = ["/post/142290881999/luks-with-key-file-on-kalidebian-jessie"]
+++

LUKS with key file on Kali/Debian Jessie
========================================

Today I managed to setup Kali (Debian Jessie) with LUKS and a key file
on a USB stick. This took me considerable time as much information on
the process is either outdated or for other Linux flavors.

When you have figured it out it is, of course, pretty easy. Let me break
it down.

First of forget all the key generation bullshit. Carrying a USB drive
with a file called 'secret\_key.bin' is immediately suspesious. Carrying
a USB drive with a whole bunch of pictures of your kids is significantly
less so. For the TLA agencies to break your encryption they need to
generate that specific picture of you at the beach. So just pick a nice
picture and keep it under 8MB as that's the maximum size of the key
file. Just to make things absolutely innocent also make it a VFAT disk.

As the next step make is easy on yourself and do an install with the
guided partitioning option with encryption. Go ahead and use the entire
disk, everything on one partition. Many opt for convoluted setups, I
believe that's only more to mess up. Besides doing a guided setup will
make sure that the encryption setup works and that you only have to add
the key file (and some other minor details).

Then there are a couple of things to know as background. You'll read
everywhere that you're supposed to edit `/etc/crypttab`. This confused
me as this file is on the to-be-encrypted disk, so how was whatever was
decrypting the disk what to do? Well, enter \'initramfs' (I fear that at
some point I'll need to read Linux From Scratch). This is the tiny
system booted into by Grub.

1.  Power on.
2.  Grub (really the only bootloader which is relevant nowadays).
3.  Initramfs.
4.  Full blow system.

This is where the outdated stuff confused me. There's talk about kernel
parameters and Grub options and custom shell scripts. None of that is
necessary. We'll be doing our business in the update to date initramfs.
Edit the `/etc/crypttab` file to point to your key file. Replace \'none'
into something like:

    root UUID=<your-encrypted-disk-uuid> /dev/disk/by-uuid/<your-usb-disk-uuid>:/path/to/keyfile luks,keyscript=passdev

(I now believe that using the UUID is a risk when your USB disk breaks
there's no way to recover. `by-label` looks saner.)

Add to `/etc/initramfs-tools/modules`:

    nls_cp437
    nls_utf8

This is to ensure the tiny system called initramfs knows how to read a
VFAT disk. All the USB modules are included by default.

Also add your keyfile to the accepted keys:

    cryptsetup luksAddKey /dev/<device> (/path/to/keyfile)

You'll need to type the initial encryption password.

Now for the magic part:

    $ update-initramfs -u

If you see the message: `target sda5_crypt uses a key file, skipped` you
have forgotten to add keyscript=passdev. This basically pipes the key
file as the password into the decryption phase.

Reboot!

You'll be greeted by the somewhat strange `a start job is running` and a
timer which counts up to 1m30. I'm unsure what to make of this other
than that is annoyingly long. If you don't have your USB key slotted it
just seems to hang (\'oh no my disk crashed!').

