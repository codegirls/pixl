# Still pixling (vectors, shapes & randomness)

Actually, more fancy things using JavaScript.

Today, we're going to make some more interesting shapes, move pixls
around and share the code we wrote.

As with last time, start by making your changes apply only locally:

```javascript
pixl.disconnectAndClear();
```

## some more interesting shapes.

Last week we wrote various kinds of lines and then the beginnings of some
other stuff. But we also want arbitrary lines (not just straight and diagonal
ones), more complex objects like rectangles and houses which are made of
lines and then other shapes like circles and ellipses.

Here are some tips:

* a line can be represented as two points. but to draw a line between two such
    points we need to figure out where our "steps" should go. to do this we
    need a (normalized) vector.

    the normalized vector represents the "step" we have to take to draw
    one pixl of the line. to get a line, we execute that step n times.

    here are two videos about vectors:

    - [Vectors Part 1](http://www.youtube.com/watch?v=DfGOw8_ZaBA)
    - [Vectors Part 2](http://www.youtube.com/watch?v=zYOGtlY6xaM)
* rectangles are quite simple, just think about them for a bit. (and maybe
    draw them empty, filled and with a checkerboard inside.)
* houses are just a rectangle and two lines. but what if we want houses with
    different heights and different types of roofs?
* circles. you can draw circles if you understand what the [unit circle](https://en.wikipedia.org/wiki/Unit_circle)
    is.
* ellipses are fun because circles are actually ellipses with the same radius
    for x and y. so if you know how to draw a  circle, ellipses should be
    easy

## random pixls!

Javascript can generate random numbers using `Math.random()`. calling that
function gives you a different number between 0 and 1 each time you call it.

You can than scale that number to correspond to a position on the screen to
draw a pixl at a random position.

```javascript
var random = Math.random();
//=> 0.9401923281947845
```

But you could also generate pixls with random colors. to do that, we need
to represent colors as numbers:

```javascript
var red = "rgb(255, 0, 0)";
```

That is, colors can be represented as three values for the red, green and
blue part of the color. But to make html, css and pixl interpret those values
as a color we have to put it into a string.

So, to generate a color we need to generate three random numbers, scale them
such that they are in the range of 0 to 255 and then put them inside a string.

```javascript
// e.g. something like this:
var r = 0, g = 255, b = 0;
var color = "rgb(" + r + ", " + g + ", " + b + ")";

pixl.draw_pixl({x: 0, y: 0}, color);
```

Note that you must `Math.round` the numbers you get before putting them into
the string.

## animation

Now that we know a bit more how colors work we can make a pixl that changes it's
color over time:

```javascript
var pos = {x: 0, y: 0};
var r = 0, g = 0, b = 0;

function animate_color() {
  pixl.draw_pixl(pos, "rgb(" + r + ", 0, 0)");

  r += 10;
}

setInterval(animate_color, 200);
```

Here `setInterval` tells the browser to call the `animate_color` function every
200 milliseconds.

Try some other things:

* changing the color from red to green to blue over time
* blinking (e.g. going from 0 to 255, back to 0 and up again. and again. and again)

## moving things around

`setInterval` (and the related `setTimeout` function) can be used to do all kinds of
things related to timeouts, so why not animate pixls moving around?

```javascript
var currentPos = {x: 0, y: 0};
var direction = {x: -1, y: 0};

function bounce() {
  var w2 = pixl.area.w2();
  if (currentPos.x < pixl.pos.x - w2 || currentPos.x > pixl.pos.x + w2) {
    direction.x = direction.x * -1;
  }
  pixl.draw_pixl(currentPos, "white");
  currentPos = {x: currentPos.x + direction.x, y: currentPos.y};
  pixl.draw_pixl(currentPos);
}

setInterval(bounce, 500);
```

Play with that, i'd like to see what you come up with. Some ideas:

* bounce in the y-direction, too
* move around faster

## and some more ideas

* make a snake!
* make a rainbow
    - maybe even a blinking rainbow
* plot a function on the screen
    - `function(x) { return 0.001 * x * x; }`
    - `Math.sin(x)`
    - `function(x) { return x % 10; }`

## sharing the code

You can share the code using the `pixl.scripts` utilities.

```javascript
// let's make a small library for dealing with random numbers
var random = {
  num: function(lo, hi) {
    return lo + Math.random() * (hi - lo);
  },

  int: function(lo, hi) {
    return Math.round(random.num(lo, hi));
  },

  color: function() {
    var r = random.int(0, 255), g = random.int(0, 255), b = random.int(0, 255);
    return "rgb(" + r + ", " + g + ", " + b + ")";
  },

  pixls: function (n) {
    var w2 = pixl.area.w2();
    var h2 = pixl.area.h2();
    for (var i = 0; i < n; i += 1) {
      pixl.draw_pixl({x: pixl.pos.x + random.int(-w2, w2),
                      y: pixl.pos.y + random.int(-h2, h2)},
                      random.color());
    }
  }
}

// and then save it
pixl.scripts.save("random", random);
```

This saves the functions to defined and passed to `pixl.scripts.save` and
makes them availlable to others.

It also makes it possible to get your functions back easily after a reload.

```javascript
pixl.scripts.load("random");

random.num(0, 100);
//=> 73.80250617330074

random.pixls(100);
```

## links

* [Coding Math](http://youtube.com/user/CodingMath/videos): simple math makes cool things,
    basically. using html canvas, keith peters demonstrates math that is useful for coding,
    using interesting examples. (for example [a simple planet system](http://www.youtube.com/watch?v=EhDtJxX0sCA).)
* and of course, if you want to do `pixl` in 3d, use [trixl](http://pixl.papill0n.org/3).
