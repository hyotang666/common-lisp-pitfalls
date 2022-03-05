# Difficult to understand.

## Ordinary, symbol name has uppercase.

```lisp
(find-symbol "car" :cl) => NIL, NIL

(find-symbol "CAR" :cl) => CAR, :EXTERNAL
```

## Return NIL when found NIL.

```lisp
(find-symbol "NIL" :cl) => NIL, :EXTERNAL
```

A typical bad example is below.

```lisp
(when (find-symbol name :cl)
  ...)
```

The code above does not work expectedly when `NAME` is `NIL`.

