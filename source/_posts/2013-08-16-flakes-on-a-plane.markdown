---
layout: post
title: "Flakes on a Plane"
date: 2013-08-16 21:19
comments: true
categories: [Testing]
---

This is a story of how coding at thirty thousand feet helped me to write more testable code.

It started out simple enough. I decided I wanted to write a static site generator in Ruby. But it wasn't going to be like all those other static generators focused on making blogs. My site generator would be a simple solution for building simple sites. That doesn't really matter though. What does matter is that I hadn't written any Ruby in years, and I was flying from Dallas to San Francisco on the day inspiration struck.

I knew how I wanted everything to work. I would read in a YAML file describing a site, then based on that file read in various other files containing Haml, Sass, CoffeeScript, etc. and spit out some ready to serve static assets. Normally this would turn into a quick and dirty hack with about a dozen tabs open in my browser as I looked up various libraries and Ruby documentation. But I was in a metal tube in the sky.

Now, I could have shelled out the money to pay for some of that WiFi they put in planes these days, but I decided that would be too easy. I took it as a challenge. I would prove that I was capable of programming without the crutch that is the Internet. This idealistic dream quickly fell apart when I realized I didn't have any of the libraries I needed. That didn't matter though. I could lie.

I set to work writing my application with complete disregard for the infrastructure I lacked. Any time I needed something I didn't have, I wrote a fake version. My editor soon filled with functions like `read_config` and `render_haml`. By the time the flight ended I had a perfectly crafted piece of logic that did absolutely nothing. But then I realized the unintentional brilliance of what I had done.

My core logic was a standalone unit with no dependencies. Every integration point had been perfectly mocked out of necessity. I had accidentally crafted the test driven ideal. All that was needed were some very minor alterations to make my fake functions easily injectable and everything was done. What started as a quick hack became a well designed testable application all because I didn't have an Internet connection.
