+++ 
draft = false
date = 2012-11-25T19:33:00+00:00
title = "A better Chef; Ansible"
description = ""
slug = "" 
tags = []
categories = []
externalLink = ""
series = []
aliases = ["/post/36524862862/a-better-chef-ansible"]
+++

A better Chef; Ansible
======================

Lots of people still use Chef for their devops needs. I briefly used
Chef about 6 months ago and got very frustrated. I find the process
convoluted and confusing. For our Riak cluster we needed a deploy script
to move an install script and resources to the remove host. The install
script installed Ruby, some required packages only *then* the actual
Chef recipe was run. Maybe I was doing it wrong, but then I'm of the
opinion that the whole thing is too complicated.

Ansible
-------

With [Ansible](http://ansible.cc) you can:

-   Run one-off commands (want to know the loadon your cluster?
    `ansible riak-nodes -m 'w'`
-   Provision servers with a simple YAML file
-   Even replace Capistrano

Ansible is opinionated, questions I have asked on the mailing list were
often quickly answered with a "you're doing it wrong". For example:

-   Adding lines to a configuration file is considered smell. This leads
    to a remote system of which the state is not clearly defined.
-   Downloading packages from a remote source? You can't be sure this
    source is still up. Download the package yourself and copy it over.
-   Downloading a tarball to compile it on the spot? Do it once and roll
    a package.

A "playbook" is the Ansible equivalent of a cookbook in Chef. It is a
play YAML file:

God bless it's simplicity. (Yes I know the playbook is still a work in
progress)

