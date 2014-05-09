---
layout: post
title: "Options for Maintaining Privacy Online"
date: 2013-06-23 20:11
comments: true
categories: [Privacy, Encryption]
---
How do you maintain privacy on the Internet? If you're anything like me you probably don't like the idea of other people having access to things like your email and search history. Luckily there are options. I can't feasibly go into detail about setting up all of these solutions, but I can at least show you what you have to work with.

##Web Browser
The first step in maintaining online privacy is understanding your browser's privacy controls. Most major browsers, such as [Firefox](https://support.mozilla.org/en-US/products/firefox/privacy-and-security) and [Chrome](https://support.google.com/chrome/answer/114836?hl=en#), have options to configure what data gets stored on your machine, as well as an option to tell web sites not to track you. Features like tab syncing are convenient, but remember that information is being stored somewhere.

##Search Engine
Most search engines keep some sort of history about your searches. If it's a search provider you are logged into, this history is probably linked to your account and not just the machine you're using. If you want to make sure your search history is private, use a search engine such as [DuckDuckGo](https://duckduckgo.com/) that doesn't store any information.

##Tor
If you want to make sure no one can see what web sites you're visiting, then you want [Tor](https://www.torproject.org/). When using Tor, your browsing activity is hidden by routing through a series of proxies. Tor is available as a browser plugin, but you can also download a pre-configured browser bundle if you want a simpler option.

##Instant Messaging
Keeping instant messages private is as simple as using a client with [OTR (Off-the-Record)](https://en.wikipedia.org/wiki/Off-the-Record_Messaging) support. Pidgin has a solid [OTR plugin](http://www.cypherpunks.ca/otr/) and Adium has support out of the box. Setting up an OTR conversation is relatively automated, you'll just need to verify that the other user is who they say they are.

##Email
While instant messaging is typically secured through OTR, email tends to be secured with the more general purpose [PGP (Pretty Good Privacy)](https://en.wikipedia.org/wiki/Pretty_Good_Privacy) encryption. PGP is a a form of [public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) that most mail clients support either natively or through plugins. Setting up PGP is more involved than OTR, but you can use it for encrypting anything.

##Common Sense
All the technology that exists to help maintain your privacy is useless without some common sense on your part. Any data you send to a web service may be stored by that service and later exposed. It's up to you to make sure any data you send over the wire is either encrypted or safe to share with the world.
