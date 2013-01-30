---
layout: post
title: "Stupid Browser Tricks : Live Editing Styles"
date: 2013-01-29 22:26
comments: true
categories: [JavaScript, CSS, HTML5]
---

The Hacker News post about creating a [one line browser notepad](https://coderwall.com/p/lhsrcq) reminded me of a neat trick [one of my friends](http://davidhollis.net/) showed me. Try loading this html into Chrome (or any browser that supports `contenteditable="plaintext-only"`).

``` html
<html>
  <head style="display: block">
    <style style="display: block"
           contenteditable="plaintext-only">
      body {
        background-color: #ccc;
      }
    </style>
  </head>
  <body>
    <h1>My style really shows...</h1>
  </body>
</html>
```

You should immediately notice the `style` element is now visible. Moreover you can edit it and see the changes reflected on the page. Because `content-editable` is set to `plaintext-only`, you can even add new lines to the `style` without pesky paragraph tags getting inserted and breaking everything.
