---
layout: post
title: "Useful Maths for Games and Stuff"
date: 2012-12-01 23:30
comments: true
categories: [JavaScript, Linear Algebra, Video Games, Computer Graphics]
---

I decided I wanted to step back a little and go over some of the fundamental math that underpins most of the projects I work on. This post is the first in a collection that aims to casually explain linear algebra functions useful for video games and similar applications. Most are simple and derive their power from building on previously established functions, so make sure to read everything in order. Because it relates to my recent and upcoming work, examples will use JavaScript.

## Scalars, Vectors, and Points! Oh My!
The fundamental constructs of linear algebra are scalars, points, and vectors. Both points and vectors are represented as objects with x, y, and if you're working in three dimensions z components. The components of a point represent a position, whereas the components of a vector represent a direction. Since JavaScript employs duck typing we can use the same structure for both, a simple object literal.

``` javascript
var point = {
    x: 3,
    y: 4,
    z: 5
};

var vector = {
    x: 3,
    y: 4,
    z: 5
};
```

### Basic Arithmetic and Equality
Now that we have points, vectors, and scalars, we can start doing some basic math. Since both are represented the same, operations like adding a point to a vector and adding a vector to a vector can use the same code.

``` javascript
// Add a vector and a point/vector
function add(a, b) {
    return {
        x: a.x + b.x,
        y: a.y + b.y,
        z: a.z + b.z
    }
}

// Subtract a vector from a point/vector
function subtract(a, b) {
    return {
        x: a.x - b.x,
        y: a.y - b.y,
        z: a.z - b.z
    }
}

// Multiply a vector and a scalar
function multiply(v, s) {
    return {
        x: v.x * s,
        y: v.y * s,
        z: v.z * s
    }
}

// Divide a vector by a scalar
function divide(v, s) {
    return {
        x: v.x / s,
        y: v.y / s,
        z: v.z / s
    }
}

// Test if two vectors/points are equal
function equal(a, b) {
    return a.x === b.x && a.y === b.y && a.z === b.z;
}
```

### Vector Length
With basic arithmetic established we can easily find the length of a vector. In two dimensions this is the same as treating the vector as the hypotenuse of a right triangle and applying the Pythagorean Theorem. In three dimensions you need simply add the z term to the equation.

```javascript
function length(v) {
    return Math.sqrt(Math.pow(v.x, 2) + Math.pow(v.y, 2) + Math.pow(v.z, 2));
}
```

### Unit Vectors
A [unit vector](http://en.wikipedia.org/wiki/Unit_vector) is just a vector with a length of one. As simple as that sounds, unit vectors are incredibly useful since they can be easily scaled to any desired length. Luckily converting a given vector to a unit vector is just a matter of dividing a vector by its length. This process is called normalization.

``` javascript
function normalize(v) {
    return divide(v, length(v));
}
```

### Dot Product
The [dot product](http://en.wikipedia.org/wiki/Dot_product) is a simple operation between two vectors. For two vectors a and b, and the angle between them theta, the dot product is equivalent to the `length(a) * length(b) * Math.cos(theta)`. This means that if you take the dot product of two unit vectors you get the cosine of the angle between them.

``` javascript
function dotProduct(a, b) {
    return (a.x * b.x) + (a.y * b.y) + (a.z * b.z);
}
```

### Parallel and Perpendicular Vectors
Computing a parallel vector is unnecessary because a vector is already parallel to itself. Testing for parallel vectors is simply a matter of testing if the normalized forms of the vectors are equal or exactly opposite.

``` javascript
function isParallel(a, b) {
    return equal(normalize(a), normalize(b)) ||
           equal(normalize(a), multiply(normalize(b), -1));
}
```

Computing a perpendicular vector involves swapping the x and y components of a vector and then negating one. After this a little bit of algebra shows that perpendicular vectors will have a dot product of zero.

``` javascript
function perpendicular(v) {
    return {
        x: v.y,
        y: -v.x
    }
}

function isPerpendicular(a, b) {
    return dotProduct(a, b) === 0;
}
```

### What's Next?
At this point we've established the basic structures and functions that underly all of linear algebra. In the next post I'll introduce the cross product, a powerful vector operation that will allow us to begin working with lines and planes. After that the focus will shift to transformations, and ultimately I'll bring everything together with practical examples of the math in action.