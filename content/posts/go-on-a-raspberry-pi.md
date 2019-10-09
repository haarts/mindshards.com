+++ 
draft = false
date = 2012-12-31T13:06:00+00:00
title = "Go on a Raspberry Pi"
description = ""
slug = "" 
tags = []
categories = []
externalLink = ""
series = []
aliases = ["/post/39300576813/go-on-a-raspberry-pi"]
+++

Go on a Raspberry Pi
====================

Recently I found myself playing with both [Go](http://golang.org) and a
[Raspberry Pi](http://raspberrypi.org). I've build a some Go programs on
my Mac but copying over the executable to the Pi did not work
(surprise!). It is actually fairly easy to crosscompile a Go binary:

    GOARM=5 GOARCH=arm GOOS=linux go build your_program.go

It's all pretty self explanatory, the one thing that confused me was the
`GOARM` variable. I'd expect the `GOARCH` to be enough. But apparently
there are different ARM types out there. A full list can be found on the
Go site under [Optional Environment
Variables](http://golang.org/doc/install/source#environment).

