# Implicitly undefined.

`SIGNAL` accepts condition datum, searching handler which is associated with the condition then returns `NIL` when any handler does not change control flow.

The specification does not say about what the handler is at the top level.

```lisp
(signal 'error) => implementation-dependent. NIL or invokes debugger.
```
