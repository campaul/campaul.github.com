---
layout: post
title: "How Not to Proxy Methods in Python"
date: 2013-01-10 23:22
comments: true
categories: [Python]
---

In object oriented design, it's common to code against some sort of interface that will be used across your application. For example, if you were making a video game (yes I have a one track mind) you might design your graphics, physics, and sound engines to all interact with an entity that conformed to an interface for describing its position. Perhaps that entity would look something like this:

``` python
class Entity(object):

    def __init__(self, x, y):
        super(Entity, self).__init__()
        self.x = x
        self.y = y

    def position(self):
        return (self.x, self.y)
```

This is pretty straightforward. Each entity has a `position` method that returns a tuple with x and y coordinates. If you were building everything from the ground up, you could easily design it all to follow this convention. In reality, you're probably going to be using several third party libraries that will need to be coerced into working together.

Let's say you lucked out with the graphics engine. It expects to see entities with a `position` method that returns a tuple of x and y. The physics engine on the other hand is looking for a method called `pos`. The sound engine is different still, looking for a `location` method. They all expect the same tuple structure to be returned, so you decide to just proxy `pos` and `location` to `position`.

## Doing it Wrong : Direct References
This is simple, right? You'll just update your `Entity` a little bit with some additional references to the `position` method.

``` python
class Entity(object):

    def __init__(self, x, y):
        super(Entity, self).__init__()
        self.x = x
        self.y = y

    def position(self):
        return (self.x, self.y)

    pos = position
    location = position
```

Now you can invoke all the various engines your game utilizes with the same entity objects.

``` python
graphics_engine.foo(entity)
physics_engine.bar(entity)
sound_engine.baz(entity)
```

This seems to work great at first. All the components of your game are able to query your Entity object using whatever method they want, and get back the result they expect. So what's the issue?

A little later you decide it would be good if you had an entity class that calculated its location relative to some parent in order to make scene graphs. If you're unfamiliar with game engines this how it's usually done. This should be pretty simple with the magic of inheritance. Just make a subclass that implements its own `position` method.

``` python
class RelativeEntity(Entity):

    def __init__(self, parent, x, y):
        super(Entity, self).__init__(x, y)
        self.parent = parent

    def position(self):
        return (self.x + self.parent.x, self.y + self.parent.y)
```

At this point you would start seeing some problems. The graphics will all be correct, but the physics and sound engines will be completely broken. While the `position` method was overwritten, `pos` and `location` are direct references to the `Entity`'s `position` method. In order to fix this using the current design you need to do more to `RelativeEntity`.

``` python
class RelativeEntity(Entity):

    def __init__(self, parent, x, y):
        super(Entity, self).__init__(x, y)
        self.parent = parent

    def position(self):
        return (self.x + self.parent.x, self.y + self.parent.y)

    pos = position
    location = position
```
    
Every class that inherits from `Entity` will need to have those two lines added. This is really repetitive and error prone. Furthermore, the need to add these lines will be non-obvious to other developers.

## Doing it Better : Proxy Methods
A better solution is to actually use proxy methods instead of making direct references. This isn't much more complicated than the original implementation.

``` python
class Entity(object):

    def __init__(self, x, y):
        super(Entity, self).__init__()
        self.x = x
        self.y = y

    def position(self):
        return (self.x, self.y)

    def pos(self):
        return self.position()

    def location(self):
        return self.position()
```

Now `pos` and `location` are their own methods, that will evaluate `self.position` at call time. This means if you override the `position` method in a subclass, the `pos` and `location` methods will call the overridden method. Now the `RelativeEntity` class only needs to define the `position` method.

## Doing it Much Better : Proxy Classes
Why stop at proxy methods. Let's go all out and make some proxy classes. The entity class will be super simple now.

``` python
class Entity(object):

    def __init__(self, x, y):
        super(Entity, self).__init__()
        self.x = x
        self.y = y

    def position(self):
        return (self.x, self.y)
```

Next define the proxy classes which will wrap a standard `Entity`.

``` python
class PhysicsProxy(object):

    def __init__(self, entity):
        super(PhysicsProxy, self).__init__()
        self.entity = entity

    def pos(self):
        return self.entity.position()

class SoundProxy(object):

    def __init__(self, entity):
        super(SoundProxy, self).__init__()
        self.entity = entity

    def location(self):
	    return self.entity.position()
```

Now you just need to wrap entities whenever you make a call to the physics or sound engines.

``` python
physics_engine.bar(PhysicsProxy(entity))
sound_engine.baz(SoundProxy(entity))
```

While this approach is significantly more verbose than just using proxy methods, it has several advantages. Code is moved out of the `Entity` class and into modular proxy classes. If you ever need to add a proxy for another system, you just create a new class. `Entity` remains clean and maintainable, while the system is a whole is made more extensible. Furthermore, the explicit nature of invoking the proxy classes makes the behavior of your code much more obvious. Everything is now easier to read, modify, and extend.