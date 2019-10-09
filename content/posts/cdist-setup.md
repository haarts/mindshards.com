+++ 
draft = false
date = 2012-01-17T19:44:00+00:00
title = "cdist - the setup"
description = ""
slug = "" 
tags = []
categories = []
externalLink = ""
series = []
aliases = ["/post/16015091140/cdist-the-setup"]
+++

cdist - the setup
=================

Configuration management
------------------------

[Cdist](http://www.nico.schottelius.org/software/cdist/) is a little
piece of software which makes setting up new servers a little less
painful. I believe the main advantage of using software like this is not
the easy setup but the fact that the process creates executable
documentation. Cdist is new when compared to
[Puppet](http://projects.puppetlabs.com/projects/puppet),
[Chef](http://www.opscode.com/chef/) and a couple of others. It appealed
to me because it's not much more that a glorified bunch of shell
scripts. The other approaches I saw required a central server, pushing
code around and not the mention the requirement that Ruby should already
be installed on the target system.

Getting started
---------------

This couldn't be easier, just clone the
[repo](https://github.com/telmich/cdist). You'll need Python3, I suggest
using [Homebrew](http://mxcl.github.com/homebrew/) instead of Mac Ports.
It took me a bit more time to understand that all my code should go in
this cloned repo. Just start typing away. The maintainer suggests
pushing to a different remote and to work on your own branch. This way a
`git pull` will bring you up to date. A valid strategy I suppose but
uncommon.

But then...
-----------

I followed the
[quickstart](https://github.com/telmich/cdist/blob/master/doc/man/man7/cdist-quickstart.text)
example but as you notice it's a link to the git repo as this is not yet
officially released. Following along is pretty easy until I hit

    $ echo '__file /etc/cdist-configured' > conf/manifest/init

What does that do?

Types
-----

The `__file` denotes a 'type', the file immediately behind it is the
argument you might pass. These two combined form an object which can be
reference later. I'll get back to that (under Dependencies).

Manifest
--------

The `conf/manifest/init` is the most important file. As far as I
understood this file contains a long case statement enumerating all your
servers. I'm just hoping you can use regular expressions or groups, all
the nodes in our Riak cluster have the same setup and I'd hate it to
list them all.

So

    $ echo '__file /etc/cdist-configured' > conf/manifest/init

will make a manifest which does little. The `__file` type will create a
file if it is not there already.

Do it already!
--------------

Assuming you can login with your SSH key as root:

    $ cdist config your-remote-server

I was momentarily confused by the `config` switch as there also is an
`install` switch which function I have yet to determine. The above
command will go to your server and configures (or installs?) it.

Dependencies
------------

More often than not you want to execute some piece of code if a
condition is fulfilled. Cdist has a special feature to declare
dependancies. You can assign a value to the variable `require`
immediately follow but the code to be executed when the condition holds:

    require="__file/etc/cdist-configured" __link /tmp/cdist-testfile --source /etc/cdist-configured  --type symbolic

This seems weird and I think it is. The advantage of doing it like this
is that you can use the magic objects created when you call a type.

### EC2

As a small side note; Cdist's OS detection does not work on Amazon's
standard AMI's. This bit me when wanting a quick, clean server to try
this out on.

