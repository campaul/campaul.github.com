---
layout: post
title: "Kill It With Fire"
date: 2013-01-17 22:41
comments: true
categories: 
---

Submitting to code reviews from my coworkers has forced me to come to terms with one of my shortcomings as a developer. I'm afraid of changing code. Whenever I'm forced to interact with a poorly written component, I often try to work around it rather than replace it. Unfortunately all of my reasons for doing this are complete bullshit.

## "I'm just conforming to the design."
By conforming to a poorly designed system I'm only increasing technical debt. If anyone ever does decide to replace the code, whatever I'm writing now is just one more thing that will need to be converted with it.

## "This will all get rewritten eventually."
Code wont fix itself, and I can't assume someone else is going to do it. If I don't start changing things here and now the code will never improve. Software development is iterative so I must live in the moment.

## "It will take too long to change."
While it may be true that implementation takes longer in the short term, the long term time savings of cleaner code will far outweigh the time saved now. Less time spent writing tests, fixing bugs, and adding features will all add up.

## "I don't know enough to change it."
Rewriting a component is the quickest way to figure out how it works, and taking the time to learn will increase my understanding of the system as a whole.

## "I might break something."
It doesn't matter if I break something. That's what version control is for. I can always revert if things go catastrophically wrong.

The future is now and I have no reason to suffer poorly designed code. No more conforming to anti-patterns. No more hiding behind abstraction layers. No more waiting on someone else to fix it. The only way software will improve is if bad code is mercilessly hunted down and destroyed. Kill it with fire.
