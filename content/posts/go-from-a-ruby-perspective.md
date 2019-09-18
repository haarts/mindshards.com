+++ 
draft = false
date = 2011-11-01T23:01:00+00:00
title = "Go from a Ruby perspective"
description = ""
slug = "" 
tags = []
categories = []
externalLink = ""
series = []
+++

Go from a Ruby perspective
==========================

**update** I wrote a [follow up
post](https://mindshards.com/posts/go-from-a-ruby-perspective-part-2).

I'm notably lacking is any C/C++ skills aside from the basic course at
the university. This is why I took up [Go](http://golang.org "Golang").
[Google App Engine](http://code.google.com/appengine/) is of interest to
me because I have prior experience with Heroku and AWS and no desire to
maintain a server capable of running Go. The pet project I use to
explore Go and GAE is on [Github](http://github.com/haarts/flipco.in)
and called [Flipco.in](http://www.flipco.in).

There are things I like about Go and GAE and things I don't. Below I'll
explain what I think is wrong with Go on GAE. TL;DR it's not ready for
anything but serious
[experimentation](http://twitter.com/#!/haarts/status/130924856752619520).

Passing of the context
----------------------

Whenever doing anything related to a GAE feature like storage a
`appengine.Context` is required. I understand why this is necessary. And
I found out that the Go community has strong feelings about 'magic' (it
doesn't like it). But passing along the context var in every function
call hardly seems optimal. This issue might boil down to my inexperience
as a Go programmer, perhaps I can set a globally accessible const (yuk)?
But if that's the case, this is a pattern often/always used, why not
include it in the GAE environment? Being the common pattern I believe it
is a mention in the documentation would improve matters.

Updating Entities
-----------------

The issue which stumped me most was the updating of `Entities`. For
example take these two data structures:

    type Coinflip struct {
      Participants []Participant
      Head         string
      Tail         string
      Done         bool
    }

    type Participant struct {
       Email string
       Seen  datastore.Time
    }

This was my first attempt which failed due to the fact that the
`Participants` property of the `Coinflip` struct can not be stored in
the datastore. I understand that enabling this would entail quite some
magic. After some help on the mailing list I made it so that it stored a
slice of pointers to keys; `[]*datastore.Key`. Downside to this approach
is that I need to write my own dereference function of this slice.
Bummer, as I'm lightyears behind the average Go core member my
dereference function is going to be far worse then one written by them.
Now I manipulate one of the `Participant` by updating the `Seen`
property (after finding it by iterating over the slice). Saving it back
to the datastore requires a `Key`! So my current dereference function
([`fetchParticipants`](https://github.com/haarts/flipco.in/blob/master/flipco.in/flipcoin.go#L134))
now not only returns a slice of `Participant` but also a same length
slice of `Key`. Having remembered the index of the iterator which I used
to find the correct `Participant` I can now use that to find the
associated Key and save the Entity. Why is this so convoluted?
`participant.Put()` should have done it. I'm very much hoping that you
are going to tell me that I'm a silly n00b and doing it thus and thus
would be far easier. (Perhaps via a
[`Query`](http://code.google.com/appengine/docs/go/datastore/reference.html)?
I don't quite grasp this yet.)

Random remarks
--------------

-   Deployment is silly when compared to Heroku.
    `$ git push heroku master` and you're done. I have my SSH private
    key on my computer so no need to auth every time (OK, once. When I
    first use my key, which is often in all kinds of projects).
-   Documentation of the `template` lib is lacking. I chose to use the
    [Mustache](http://mustache.github.com/) lib instead. That took very
    little time understanding while the template lib took too much time.
-   [Exuberant ctags](http://ctags.sourceforge.net/) doesn't work with
    Go which is a shame, Vim just doesn't work as well then. I found
    some efforts to fix this which are in dubious states. Probably
    [`gocode`](https://github.com/nsf/gocode) then, but that is yet an
    other tool raising the barrier to entry in my view.
-   Rendering responses takes long long lines. For example:
    `fmt.Fprint(w, mustache.RenderFile("./flipco.in/views/layout.html", map[string]string{"body":mustache.RenderFile("./flipco.in/views/home.html", map[string]string{"title":"Awesome coin tosses - Flipco.in", "nr_of_flips":fmt.Sprint(count)})}))`.
    This only has one type in the map if a collection is required things
    get even longer. But again, my inexperience might be to blame. Only
    recently I found out about the empty interface type which might be
    of use here.

Now it might seem that I have a lot of gripes with Go and GAE. There are
also many things I like. Just to name a few, thus far I found nothing in
the Go language I dislike and compared to maintain an own server GAE is
great.

