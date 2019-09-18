+++ 
draft = false
date = 2011-10-03T17:14:00+00:00
title = "Aeroponics system live"
description = ""
slug = "" 
tags = []
categories = []
externalLink = ""
series = []
+++

Aeroponics system live
----------------------

Today the rucola growing machine went operational. How came this project
to be?

I've always been interested in plants and electronics and recent
developments gave me the opportunity to finally explorer the two. A blog
post by [an Ultrasonic Aeroponics
system](http://www.inventgeek.com/2011-Projects/Ultrasonic-Aeroponic-System/Overview.aspx)
gave me all the pointers I needed. Almost all aspects of the project are
better described there so I suggest you read that post first. Excellent
reading!

### Differences

#### Time

It took me a bit longer to build the project this being my first of this
kind. I spent a couple of days on it. Mostly on the Arduino.

#### Setup

One major difference that I use an Arduino clone ([a
Jeenode](http://jeelabs.org)) to turn the mister on and off. InventGeek
didn't include that in their design but it seems pretty common to do so.
This lets the root aerate. Currently I run the fogger for 5 minutes
every half an hour.

#### Costs

I had to buy everything from scratch and I was unable to find a mister
*and* a power supply for \$6. I spend nearly \$20 dollars on that alone.
Here's a [complete
breakdown](https://docs.google.com/spreadsheet/ccc?key=0AnaTiZjJ-EphdEQxY0VPVExxWVVnVzFIY05OcFNaR1E&hl=en_US).

Future
------

Now I have only optimized one part of the growth process namely nutrient
uptake. Evidently ambient temperature and light are just as important. I
wish I had a server running at home. That waste heat would have been
excellent. For lighting I'll research these LED grow lights on eBay.

Using an Arduino for just a timer is silly. I plan to measure ambient
temperature, lighting conditions and acidity of the water in the near
future and push those measurements in a small database and make some
pretty graphs.


