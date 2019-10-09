+++ 
draft = false
date = 2012-03-16T15:01:00+00:00
title = "Use RSpec to monitor your app"
description = ""
slug = "" 
tags = []
categories = []
externalLink = ""
series = []
aliases = ["/post/19396434337/using-rspec-to-monitor-your-apps"]
+++

Using RSpec to monitor your apps
================================

RSpec did it again. It blew my mind. Just when I was doubting how
awesome it was.

At [Skylines](http://skylin.es) we run a *lot* of services. API's,
websites, apps. You name it. When something goes down we want to know
about it. Not when a client calls but the second after it breaks.

As a good developer you write a bunch of (unit/integration) tests. These
tests are used when writing the code. But when the code is deployed all
bets are off.

Our applications have a lot of moving parts and when one breaks that
impacts our user experience. We want to monitor the experience our users
are getting. It our API still up? Does it return valid JSON? Contains
the JSON returned the fields we expect it to hold?

These questions sounded eerily like your run of the mill RSpec tests. I
saw two problems with RSpec. Unlike regular tests we wanted to run tests
continuously on live applications. Also RSpec just outputs on the
console whether or not a test failed, we want to receive emails/texts
when stuff breaks.

Turns out these aren't problems at all! Years ago David
[wrote](http://blog.davidchelimsky.net/2010/06/14/filtering-examples-in-rspec-2/)
about the metadata properties you could pass to a `describe` or `it`
method. Turns out this is ideally suited for what we want. Flag an
example (or example group) as being a live test:

    describe "live tests", :run_live do
      it "should return a 200 status code" do
        response = Curl::Easy.http_get("http://google.com")
        example.metadata[:live][:time_to_first_byte] = response.start_transfer_time
        response.header_str.should =~ /200 OK/
      end

      it "should return valid JSON"
      it "should have some fields in the JSON"
    end

And in spec\_helper.rb:

    config.after(:each, :run_live => true) do |example_group|
      #do whatever you like with the exception and possible metadata
      example_group.example.exception
      example_group.example.metadata[:live]
    end

All we need now is a daemon on some random server which checks out every
repo we have and periodically run:

    $ rspec -t run_live

Happy.

