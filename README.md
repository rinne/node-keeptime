IN A NUTSHELL
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

METHODS
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


AUTHOR
======

Timo J. Rinne <tri@iki.fi>


LICENSE
=======

GPL-2.0