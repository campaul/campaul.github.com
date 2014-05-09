---
layout: post
title: "Creating a Modal Dialog with One Line of jQuery (and a Little Bit of CSS)"
date: 2012-10-14 01:30
comments: true
categories: [JavaScript, CSS]
---

Are you tired of dealing with bloated and/or broken JavaScript lightbox libraries? I am, especially considering all I need is a simple modal dialog. The basic idea is to create a div (or some other element) that sits centered in the window on top of all the other content on the page. Luckily this can be achieved with very little code.

## HTML
I'm going to go for a lightbox style modal popup that darkens the page while active. The markup for this is straightforward and involves a `div` for the background and a `div` for the modal dialog.

``` html
<div class="modal-background">
    <div class="modal-body">
        Lorem ipsum ...
    </div>
</div>
```

## CSS
Most of the heavy lifting will be done by the CSS. The background will be a fixed position element with `top`, `bottom`, `left`, and `right` all set to zero, as wall as a translucent background color. The modal dialog is similarly a fixed position element, but with a fixed size as well. It is centered by setting `left` and `top` to fifty percent and then using `margin-top` and `margin-left` to shift it back half its width and height. Finally, both elements are set to `display: none` so they are not visible on page load.

``` css
.modal-background {
    position: fixed;
    left: 0;
    top: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, 0.75);
    display: none;
}

.modal-body {
    position: fixed;
    width: 640px;
    height: 480px;
    left: 50%;
    top: 50%;
    margin-left: -320px;
    margin-top: -240px;
    background: #fff;
    display: none;
}
```

## jQuery
Now that all of that is set up, we get to the single line of jQuery. All this does is show the elements. If you don't want fancy animations (or don't mind coding your own) you can easily get away without using jQuery.

``` javascript
$('.modal-background').fadeIn().find('.modal-body').slideDown();
```

While you can technically create the modal using one line of jQuery, you will need a second line to destroy it.

```javascript
$('.modal-background').fadeOut().find('.modal-body').slideUp();
```

There are obviously several limitations to this one line approach, but the styles for the modal can be easily used to develop a more comprehensive solution.
