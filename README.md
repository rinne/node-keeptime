In A Nutshell
=============

KeepTime is a simple class to make time measurements in node.js.

In a simple case, time can be measured just by:

```js
var kt = new KeepTime(true); // timer is autostarted
... // your own code here
console.log('code took ' + kt.get() + ' seconds to run.');

Somewhat more complex measurement:

var kt = new KeepTime(); // timer is not started
for (var i=0; i<42; i++) {
    ... // do something non-interesting here
    kt.start();
    ...
    // do something time critical and interesting here
    // and measure the time cumulatively
    ...
    kt.stop();
    ... // do something non-interesting here
}
console.log('code took ' + kt.get() + ' seconds to run.');
```

Methods
=======

KeepTime(autoStart)
-------------------

The constructor method that is used to create a timer object. The
timer can optionally be created in automatically started state. If
called without argument or with argument evaluating to false, the
timer is created in stopped state.

KeepTime.prototype.get()
------------------------

Look up the current time from a timer and return the time the timer
has been running in seconds.

KeepTime.prototype.set(seconds)
-------------------------------

Set the timer to given number of seconds. Only finite, non-negative
numbers are allowed.

Avoid using ridiculously high values. get() returns a floating point
number of seconds, so its resolution is a nanosecond or better only
below 2^23 seconds (about 97 days). At 2^40 seconds (about 35 000
years) it is about a quarter of a millisecond. getArray() always has
nanoseconds. set() keeps the fraction of a second up to about 9e14
seconds (28 million years) and rounds to whole seconds above that.

KeepTime.prototype.getReadable(decimals)
----------------------------------------

Look up the current time from a timer and return the time the timer
has been running in a readable string with given number of decimals
after seconds. Maximum number of decimals is 9 and the default is 0.

If the time is less than one hour (i.e. 3600 seconds), it's is
returned in form 'mm:ss' (followed by possible decimals like other
formats). If the time is less than one day, it's returned in format
'hh:mm:ss'. If it's more than a day, it's returned in format
'd+hh:mm:ss'. For time values larger than one year, approximate number
of years is added to the string. For ridiculously big values, only
approximate number of years is returned and smaller units are omitted
altogether, which naturally causes also decimals to be ignored.

In case the least significant parts of the timer value is beyond the
precision of number type, the return value is padded with zeros rather
than arbitrary digits.

KeepTime.prototype.getArray()
-----------------------------

Look up the current time from a timer and return the time the timer
has been running as array of two integers. The first number is seconds
(rv[0] >= 0) and the second number is fraction of second in
nanoseconds (0 <= rv[1] < 1000000000).

KeepTime.prototype.stop()
-------------------------

Stop the timer. While the timer is in stopped state, the calls to get
and getArray methods return the same value unless reset is called in
between.

KeepTime.prototype.start()
--------------------------

Start (or resume) the timer.

KeepTime.prototype.reset()
--------------------------

Reset the time of the timer to zero. The call does not affect on the
run state of the timer (i.e. running timer remains running and stopped
timer remains stopped).

KeepTime.prototype.isRunning()
------------------------------

Return true if the timer is running, false if it's stopped.

KeepTime.prototype.toString()
-----------------------------

The same as getReadable(6), so that a timer can be used directly in a
string.

KeepTime.readable(seconds, decimals)
------------------------------------

A static version for converting a number of seconds to a readable
string.

KeepTime.isKeepTime(value)
--------------------------

Return true if the value is a KeepTime object, false otherwise.

Author
======

Timo J. Rinne <tri@iki.fi>


License
=======

GPL-2.0
