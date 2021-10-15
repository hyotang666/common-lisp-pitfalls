# Implicitly undefined.
When slot init value is not specified, such slot status is undefined.

```lisp
(simple-condition-format-control (make-condition 'simple-condition))
=> Undefined, NIL or ERROR slot-unbound.
```
