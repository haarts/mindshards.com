+++ 
draft = false
date = 2013-01-18T08:18:00+00:00
title = "Expectations in a RSpec before filter"
description = ""
slug = "" 
tags = []
categories = []
externalLink = ""
series = []
aliases = ["/post/40829188533/expectations-in-a-rspec-before-filter"]
+++

Expectations in a RSpec before filter
=====================================

Last week I found a piece of code which put expectations (for example
`should_receive` or the likes) in before filters in your spec file. I
believe this is not correct in subtle ways.

-   A before filter is meant to define the 'world' your RSpec is going
    to run in. Not to set expectations. These go into `it` blocks.
-   Besides that, when putting expectations in a `before` filter, the
    expectation is needlessly checked ever `it` block. Imagine the
    expectation *not* being met. All of the sudden all your specs turn
    red. I'd rather see a specific spec fail so I immediately know where
    to look.

So I'm suggesting to put no expectations in your `before` filters and if
you feel the urge to do so it probably needs it's own `it` block.

An example of how it should be done:

    describe "foo" do
        before do
            some_object.stub(:some_method).and_return(:some_value)
        end

        it "manipulates the object" do
            some_object.should_receive(:some_method).with(:some_argument)
            some_invocation
        end
    end

