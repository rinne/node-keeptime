Changelog
=========

1.6.1
-----

- README: the precision of large timer values was described wrongly
  (2^40 seconds is about 35 000 years, not 6e32, and get() loses
  nanosecond resolution already above about 97 days). toString() and
  KeepTime.isKeepTime() are documented.
- The tests are no longer included in the published package.

1.6.0
-----

Requires Node.js 4 or newer (the code already needed it).

- `set()` with an invalid or negative value threw `ReferenceError:
  e is not defined`. It now throws a `TypeError` ("Bad timer value")
  or a `RangeError` ("Can't set timer to negative value").
