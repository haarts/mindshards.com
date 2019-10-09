+++ 
draft = false
date = 2013-05-30T14:17:00+00:00
title = "Creating functions in Fish"
description = ""
slug = "" 
tags = []
categories = []
externalLink = ""
series = []
aliases = ["/post/51719448462/writing-functions-in-fish"]
+++

Creating functions in Fish
--------------------------

### Variable declarations

Variables in Fish might be a bit counter intuitive for some one with a
programming background. It is done with the
[set](http://fishshell.com/docs/2.0/commands.html#set) buildin. The
plain `set galaxy_destroyers` does one of two things depending on the
global state of the shell.

1.  If there is already a global variable with the name
    `galaxy_destroyers` invokation of `set galaxy_destroyers 42` changes
    that variable to 42.
2.  If there is no such variable invokation creates a local variable
    with said value.

To avoid this ambiguity it is wise to use `set` with the `-l` flag in
your functions. This forces the variable to be local (with a twist...).

When following this best practice you'd might be temped to do:

    function galaxy_destroyer
       if test 1 -eq 1 # always true
         set -l destroyer 234
       end
       echo $destroyer
     end

    $ sheep
    > 234

This works!

However:

    function last_destroyer
      set -l destroyers dalek cylon borg
      for i in $destroyers
        set -l last $i
      end
      echo $last
    end

    $ herd
    >

This returns nothing! That is because the `if` clause does not introduce
a new scope but the `for` clause does. Using the `-l` flag makes the
variable local to the scope.

To avoid these subtle errors you often see the variables declared in a
function like so:

    function herd
      set -l destroyers
      ...
    end

This concludes part 1. In the next part I'll elucidate return types in
Fish.

