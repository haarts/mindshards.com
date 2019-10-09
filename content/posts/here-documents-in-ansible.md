+++ 
draft = false
date = 2012-12-02T21:00:00+00:00
title = "Here documents in Ansible"
description = ""
slug = "" 
tags = []
categories = []
externalLink = ""
series = []
aliases = ["/post/37052126815/here-documents-in-ansible"]
+++


Here documents in Ansible
=========================

Sometimes you have a binary which *insists* on asking you questions when
installing it. I ran into that with the linux
[Crashplan](http://crashplan.com/) installer.

Of course there is a solution to this, called ['here
documents'](https://en.wikipedia.org/wiki/Here_document). This allows
you to issue commands to a script or program by piping in a piece of pre
formatted text. Usually the CR/enter/return is represented as a just
that. Create the here document with enters at the appropriate places.

With an ansible script that is not possible. Luckily you can use `\n` in
these cases:

    ansible hostname -i ~/ansible_hosts -m shell -a "/some_path/install.sh <<EOF\nanswer to question 1\nanswer to question 2\nEOF"

Not that there are 3 `\n`'s. You need an additional one after the first
EOF.

