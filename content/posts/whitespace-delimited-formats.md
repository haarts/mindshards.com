+++ 
draft = false
date = 2013-07-10T09:28:00+00:00
title = "Whitespace delimited formats"
description = ""
slug = "" 
tags = []
categories = []
externalLink = ""
series = []
aliases = ["/post/55071359024/whitespace-delimited-formats"]
+++

Whitespace delimited formats
============================

Recently I've had the opportunity to dabble with Python, the whitespace
delimited variant of Ruby.

I always felt whitespace delimited formats are unwieldy, now I know they
are. For one, your editor can't help you.

    def sheep():
      a = 123

When pressing 'enter' just after the \'3', is your method done? Your
editor can't know and thus can de-indent. Even typing a new \'def' won't
help you as this is valid Python. Stupid.

Then there are the no-op methods (granted: a small thing). But imagine
sketching out a program. You can't leave the method bodies empty:

    def sheep():

    def herd():

This is an IndentationError. You'll have to use the language keyword
\'pass' to make this valid Python. Ugh.

To end this on a positive note; I really *do* like the list
comprehensions in Python. Nice and clean:

    [ transform(item) for item in items ]

