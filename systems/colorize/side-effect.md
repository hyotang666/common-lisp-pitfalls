# Not documented.

Colorize prints traces to `*trace-output*`.

To disable it, bind `*trace-output*` with null-dev.

```lisp
(let ((*trace-output* (make-broadcast-stream)))
  ...)
```
