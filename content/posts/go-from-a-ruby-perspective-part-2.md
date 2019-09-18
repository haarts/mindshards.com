+++ 
draft = true
date = 2011-11-04T12:15:00+00:00
title = "Go from a Ruby perspective part 2"
description = ""
slug = "" 
tags = []
categories = []
externalLink = ""
series = []
+++

Go from a Ruby perspective part 2
=================================

In a previous post about [Go and
GAE](https://mindshards.com/posts/go-from-a-ruby-perspective)
I discussed some features of the Google Appengine which didn't appeal to
me. [Andrew Gerrand](http://twitter.com/#!/go_nuts) was kind enough to
explain.

Updating Entities
-----------------

For [Flipco.in](http://www.flipco.in) I use the following structs:

    type Coinflip struct {
      Participants []*datastore.Key
      Head         string
      Tail         string
      Done         bool
    }

    type Participant struct {
       Email string
       Seen  datastore.Time
    }

In this case you need to dereference your Participants when using them.
With the `ancestor` feature of the datastore, as Andrew pointed out, it
is not even necessary to store the Participants property.

When storing a new Participant pass a Key as parent:

    key := datastore.NewKey(c, "Participant", email, 0, coinflipKey)

Fetching them becomes far easier:

    i := datastore.NewQuery("Participant").Ancestor(coinflipKey).Run(c)

This returns an `*Iterator`. Good times.

Heroku style deployment
-----------------------

I hold this against myself. [Not everyone uses
Git](http://qa.debian.org/popcon-graph.php?packages=git++git-core+mercurial+bzr+darcs+cvs+subversion+monotone&show_vote=on&want_legend=on&from_date=&to_date=&hlght_date=&date_fmt=%25Y-%25m&beenhere=1).
Hell, I toyed with Mercurial a couple of days back. Deploying with a VCS
agnostic tool is a good idea.

Excellent example Go code
-------------------------

Learning a new language means reading a lot of code. The hard part is
finding good code to read. Andrew was kind enough to point out a
[repo](http://code.google.com/p/go-ray/) which he wrote himself
demonstrating lots of cool Go and GAE features.

In terms of documentation Go on GAE has some way to go. Which is why I'm
writing about it. I'll be updating Flipco.in.

