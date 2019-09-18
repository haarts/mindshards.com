+++ 
draft = false
date = 2013-05-30T14:41:00+00:00
title = "Creating functions in Fish part 2"
description = ""
slug = "" 
tags = []
categories = []
externalLink = ""
series = []
+++

Creating functions in Fish part 2
================================

set -l commits (git rev-list --left-right \$upstream...HEAD \^/dev/null;
set os \$status) if test \$os -eq 0

There is no name scoping in Fish. So we prefix all method with the
'class'/\'scope.

