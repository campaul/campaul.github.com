---
layout: post
title: "Extending LiterallyCanvas: Creating New Shapes and Tools"
date: 2012-11-23 23:18
comments: true
categories: [LiterallyCanvas, HTML5, Canvas, CoffeeScript, jQuery]
---

We designed [LiterallyCanvas](http://literallycanvas.com) to be as extensible as possible, and I'm going to show you just how easy to add new functionality to the plugin by creating a tool to draw rectangles. This functionality will soon exist out of the box (if it doesn't already), but for the sake of providing an easy to understand example pretend it doesn't.

To start off, I'm going to create a `Rectangle` class which will extend the built in `Shape` class. You can put this class anywhere you want, but I'm going to put it in the LC namespace.

``` coffeescript
class LC.Rectangle extends LC.Shape

  constructor: (@x, @y, @strokeWidth, @color) ->
    @width = 0
    @height = 0
    
  draw: (ctx) ->
    ctx.lineWidth = @strokeWidth
    ctx.strokeStyle = @color
    ctx.strokeRect(@x, @y, @width, @height)
```

That's it. All you need to do is provide a `draw` method that accepts a 2D graphics context and draws somthing. Now we just need a `Tool` to create new `Rectangles`. There are several things you can override from the `Tool` class, so I'm just going to explain them in comments below.

``` coffeescript
class LC.RectangleTool extends LC.Tool

  construtor: ->
    @strokeWidth = 5
  
  # The title of the tool
  # This will appear on the toolbar button's tooltip
  title: "Rectangle"
  
  # The suffix for the CSS class applied to the toolbar button
  # In this case the button will have the class "tool-rectangle"
  cssSuffix: "rectangle"
  
  # Returns the contents for the toolbar button
  # This should probably be a 24x24 pixel image
  buttonContents: -> $('<img src="img/rectangle.png">')
  
  # Returns the contents for the tool's options UI
  # See the Pencil tool in literallycanvas/coffee/tools.coffee
  # for an example of creating a slider to change @strokeWidth
  optionsContents: -> # Not implemented in this example
  
  # Called when the user starts drawing
  # eg. mousedown, touchstart
  # lc is the LiterallyCanvas instance
  begin: (x, y, lc) ->
    @currentShape = new LC.Rectangle(
      x, y, @strokeWidth, lc.primaryColor)
    
  # Called when the user continues drawing
  # eg. mousemove, touchmove (dragging detection is handled)
  # lc is the LiterallyCanvas instance
  continue: (x, y, lc) ->
    @currentShape.width = x - @currentShape.x
    @currentShape.height = y - @currentShape.y
    lc.update(@currentShape)
    
  # Called when the user finishes drawing
  # eg. mouseup, touchend
  # lc is the LiterallyCanvas instance
  end: (x, y, lc) ->
    lc.saveShape(@currentShape)
```

For efficiency, all the existing shapes are rendered to an offscreen bufffer. As the user is drawing a new shape, `lc.update` is called to repaint the new shape over the buffer. This is preferable to redrawing all of the existing shapes individually as the user moves the mouse (or their finger). When the user finishes drawing, `lc.saveShape` is called to add the new shape to the list of existing shapes.

Now that we have a `Shape` and a `Tool` defined, all we need to do is tell the plugin to use them. This is done at invocation.

``` coffeescript
$('.literally').literallycanvas({
  toolClasses: [LC.Pencil,
                LC.Rectangle,
                LC.Eraser,
                LC.Pan,
                LC.EyeDropper]
});
```