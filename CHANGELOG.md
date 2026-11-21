Changelog
=========

1.6.0
-----

Requires Node.js 4 or newer (the code already needed it).

- `set()` with an invalid or negative value threw `ReferenceError:
  e is not defined`. It now throws a `TypeError` ("Bad timer value")
  or a `RangeError` ("Can't set timer to negative value").
