---
layout: post
title: "It's Literally a Canvas"
date: 2012-11-22 23:14
comments: true
categories: [HTML5, Canvas, CoffeeScript, jQuery]
---

At the risk of becoming cannon fodder for the Grammar Nazis, I'm going to talk about some work I've been doing recently turning HTML5 Canvas into a literal canvas. The project, aptly named [LiterallyCanvas](http://literallycanvas.com/), is an open source jQuery plugin that turns an HTML5 Canvas element into a tool you can paint with.

## Origin
The project started on a Saturday night when [Steve Johnson](http://steveasleep.com) approached me about helping him build an open source drawing app using HTML5 and CoffeeScript. I needed an activity for the night, so I accepted and we dove into hacking something together.

Two weeks of hacking nights and weekends have passed and the project is actually starting to resemble what we envisioned. While the functionality looks fairly minimal, some cool features have already started to surface.

## Touch Support
From the very beginning one of the goals of the project was to have fantastic iPad support. The iPad (and other tablets) are ideal hardware platforms for casual drawing, so ignoring them would be a mistake. While touch support isn't yet as perfect or full featured as I want it to be, it is present and it is a high priority going forward.

Bonus: This afternoon I learned that Wacom makes browser plugins for their tablets. It is now a personal goal of mine to add solid Wacom support to the project (including use of pressure sensitivity if possible).

## Path Smoothing
LiterallyCanvas currently implements something close to a cubic B-Spline for path smoothing and calculates this curve as you're drawing. This presented enough technical challenges that I'm going to give it a separate blog post later, but for now just rest assured that your drawings will be silky smooth.

## Upload to Imgur
There isn't really much explaination for this one. LiterallyCanvas can upload your drawing directly to Imgur. It wasn't tough to add but it's damn cool and no other drawing app I've seen has this feature.

## Extensibility
We want LiterallyCanvas to be easy to extend and contribute to. The code is by no means perfect, but it's easy to modify and even now has pluggable tools (a feature which will also get another blog post). And did I mention it's open source? In case you missed the first link, check out the [LiterallyCanvas Github Project Page](http://literallycanvas.com/) to get the code, learn more about the project, and maybe contribute something if that's what you're into.