# More pixling

Today we're going to write some JavaScript. 
We will continue using [pixl](http://pixl.papill0n.org), 
but instead of clicking around to draw something, we will draw it using JavaScript.

## what's JavaScript

A programming language that comes with every modern browser and which almost every website uses in some way.

For the stuff we're going to do today, we only need a small part of JavaScript.
I'll explain what we need to know, but if you want to know more or continue on your own, 
then you might want to read one of the following:

* [Codecademy: JavaScript Track](http://www.codecademy.com/tracks/javascript)
* [Eloquent JavaScript](http://eloquentjavascript.net/index.html)
* or just continue playing and search for something when you don't
    know something. (that's how most programmers start learning.)

## javascript 101

The following examples can all be run from the browser console, which you can open with `Ctrl + Shift + I` or `Cmd + Alt + K`.
To run them, open the console and type the code you see below in the console and type `Enter` to run it.
I recommend that you really type it out instead of copying it so you remember what you did better and have the chance to make some mistakes.

Mistakes: you're learning, so you'll be doing lots of them.
If there isn't anything that doesn't trip you up, 
then you probably already know quite a lot and could help the others or do more experiments.

Let's get started.

### by running some code

All the `pixl`s that are drawn are actually shared to all other users as you draw them.
For experimenting around, it is better to disconnect and draw on your own and 
then come back online and show the others what you did.

Go to [pixl](http://pixl.papill0n.org) in your browser, open the console and type the following to disconnect:

```javascript
pixl.disconnectAndClear();
```

Now you can play around as much as you want and noone else's drawings will get overdrawn.

### ... with an example

Let's draw a horizontal line. in the console, type the following 
(use `shift-enter` to go to a new line without executing the code you typed so far.
only type enter when you have typed all of it.)

```javascript
function horizontal_line(start, length) {
  var y = start.y;
  for (var x = start.x; x < start.x + length; x += 1) {
    pixl.draw_pixl({x: x, y: y});
  }
}

horizontal_line({x: 0, y: 0} , 10);
```

As you may have guessed, the code above draws a line.
It first defined a *function* to do that and then *called* that function with two *parameter values*.
When a function is being called, javascript assigns the given parameter values to the *parameters*
and then "jumps" inside the function and executes the code in it.

Functions are wonderful. You just define them once and then can refer back to them and call them with different parameters.
If you do that with the function above it will draw lots of lines all over your screen.

Try calling the function with different parameters.

**(do it :)**

Calling the function works a bit like the following: 
first you assign the parameter values to the parameters to give them names and then you execute the *body* of the function:

```javascript
// assign the parameters
var start = {x: 0, y: 0};
var length = 10;

// execute the body of the function
var y = start.y;
for (var x = start.x; x < start.x + length; x += 1) {
  pixl.draw_pixl({x: x, y: y});
}
```

Now, what about that `for(var x = ...; x < ...; x += ...) { ... }` thing?
That's a *for-loop*. it executes it's body (what's inside the curly braces) until a *condition* is `true`.

What we want to do is draw a horizontal line. If you move your mouse around you'll notice
that the numbers in the bottom right of the pixl window change.
Those are the coordinates (x and y) of the mouse. so if you want to draw a pixl
then you call `pixl.draw_pixl` and pass those coordinates to it:

```javascript
pixl.draw_pixl({x: 0, y: 0});
```

To draw a horizontal line the `x` coordinate has to grow.
We could do that by repeating the line above with different values for x, but that's no better than clicking.
We want the computer to do it. so instead of repeating that line we make the computer repeat it by writing a for loop.

The loop in `horizontal_line` above basically does the following: set `x` to
the `start` position we passed to the `horizontal_line` as a parameter and then
increment `x` until we drew enough pixls.

To see what's going on, try executing the following:

```javascript
for (var x = 0; x < 5; x += 1) {
  console.log(x);
}
```

If you try to repeat what the computer did, then it would probably look like this:

```javascript
console.log(0);
console.log(1);
console.log(2);
console.log(3);
console.log(4);
```

Try doing the same "repeat what the computer did" for the `horizontal_line` function.

If you understand what it does, what about one of the following?

* write a function called `vertical_line`. (think about what would have to
    change compared to `horizontal_line`.)
* what about a function that draws a dotted line?
* or a function that draws a rectangle?

        ```javascript
        // rectangle(start, width, height)
        rectangle({x: 0, y: 0}, 10, 10);
        ```
* `circle(center, radius)` and `ellipse(center, radius)` are also fun.
    (ellipse would be called like this: `ellipse({x: 0, y: 0}, {x: 10, y: 5}))`)

and of course, try drawing something bigger with the functions we wrote.

### phew.

If you didn't know anything about javascript, variables, functions and all those
things before this might be quite a bit overwhelming. Don't worry, it'll go away
until you start discovering the next confusing thing. :)

If you want to know more, one of the following may help:

* [Codecademy: JavaScript Track](http://www.codecademy.com/tracks/javascript)
* [Eloquent JavaScript](http://eloquentjavascript.net/index.html)
* or just continue playing and search for something when you don't
    know something. (that's how most programmers start learning.)

And of course you can always ask anyone here what anything means or how it works.
Just make sure to quickly google it first and ask if that's confusing too.

## there's still more, of course.

Not only there's [pixl](http://pixl.papill0n.org), now there's also
[trixl](http://pixl.papill0n.org/3)!
