+++ 
draft = false
date = 2013-03-23T14:15:00+00:00
title = "Chromebook as a development machine"
description = ""
slug = "" 
tags = []
categories = []
externalLink = ""
series = []
aliases = ["/post/46068408390/chromebook-as-a-development-machine"]
+++

Chromebook as a development machine
===================================

**Update** followup: [One month
in](http://haarts.tumblr.com/post/49008909173/chromebook-development-machine-1-month-in)

I drank the cool-aid and bought a Samsung ARM Chromebook. My Macbook Pro
needed repairing and I can't go without a laptop for two weeks. For a
living I am a Ruby on Rails developer, most of my time I spent on either
the commandline and Vim or in a browser. I figured I just as well might
get a Chromebook which only has these two things. My plan was to use
plain Chrome OS with a VPS. I really didn't want to install Ubuntu on
the laptop. In the end the only thing I tweaked on the Chromebook itself
was to run it in developer mode.

VPS
---

Recently I have gotten quite enthusiastic about the devops tool
[Ansible](http://ansible.cc) which I now use to provision my VPS. I
decided to do this not only because I liked Ansible but also because
there are so many different VPS vendors out there, I wanted to be able
to quickly and painlessly switch from one vendor to the other. Currently
I rent a 2GB VPS from [BudgetVM](http://budgetvm.com/linux-vps.php) for
\$10 a month. Initially I was looking for a 4GB VPS but the price point
was more important to me and who knew how my RAM I would need? After
having run this setup for a couple of days I think 2GB is more than
enough, actually I now think the order of importance is: latency, disk
IO, CPU, RAM. What helped me enormously was
[Serverbear.com](http://serverbear.com), this site finally gave me
insight in the overgrown VPS market (and they have coupons too!).

### Ruby

Many people are compiling Ruby from source for their servers. I think
that is silly to say the least. Initially I set out to create my own
Ubuntu Ruby packages, this is not for the faint of heart and I was
struggling. Then I found [Brightbox](http://brightbox.com/), bless them!
These guys are maintaining a
[PPA](https://launchpad.net/&;brightbox/+archive/ruby-ng) with the
latest and greatest Ruby builds (also an experimental PPA). They even
threw in some
[optimizations](http://blog.brightbox.co.uk/posts/next-generation-ruby-packages-for-ubuntu).
This saved me hours.

Development
-----------

### Shell

Lots of road bumps! I have tried 'crosh' the native shell of Chrome OS
and I have tried [Secure
Shell](https://chrome.google.com/webstore/detail/secure-shell/pnhechapfaindjhompbnflcldabbghjo?hl=en).
The main downside of crosh is the it runs in a tab which then eats your
Ctrl-W. I really need that. I have twiddled with vim bindings and I
might get back to it but for now I have settled for Secure Shell. The
latter one makes it easier to store your ssh keys, which, by the way, I
had to generate on a different machine (unless you run in Chrome OS
developer mode).

### Windows

I also struggled with a setup in which I could use my windows
effectively. On my Macbook I used iTerm which had several tabs. Running
Secure Shell in a tab is not possible which it eating Ctrl-W so I run
that in a window. For a tabs substitute I now use
[tmux](http://tmux.sourceforge.net/), I'm still getting used to it. So
now I only have 2 windows between which I can cycle with \'alt-tab'. One
running Chrome and the other running Secure Shell. I find it very
important that with one particular keystroke I always get to the same
spot.

Downsides
---------

### Music

I still haven't found a proper way of playing my tunes. I have a large
iTunes library but I would be willing to switch to some online service
for less than \$10 per month. For now I resort to online radio which
involves Flash players. These are no fun at all and cause the load on my
Chromebook to steadily rise to around 3.5 at which point things start to
slow down noticeably.

### Downloads

I receive email, sometimes even with an attachment. This I can download
but what to do with a `.xsd` file? What I would really like is for my
Downloads folder to be mounted on my VPS.

My resources
------------

### Provisioning

In my [vps-ansible-config](https://github.com/haarts/vps-ansible-config)
repo all provisioning comes together. It does:

-   install Ruby
-   add new user
-   install basic packages
-   fixes locale
-   sets up my dev environment
-   links up my dotfiles

### Dotfiles

I have seriously spent time on my
[dotfiles](https://github.com/haarts/dotfiles). I have files for:

-   vim
-   zsh
-   git
-   tmux

