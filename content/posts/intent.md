+++ 
draft = false
date = 2013-06-24T12:06:00+00:00
title = "Code intent"
description = ""
slug = "" 
tags = []
categories = []
externalLink = ""
series = []
+++

# Code intent

The code below does not convey intent. And it has side effects.

```
def show 
  discussion 
end
```

```
def discussion
  \@discussion \|\|= Discussion.find 
end

