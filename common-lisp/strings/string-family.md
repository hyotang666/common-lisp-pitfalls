# Difficult to understand.

STRING family accepts a string-designator.
It means can accept characters and symbols too.

```lisp
(string= () "NIL") ; => T
(string-equal :a #\a) ; => T
```

If you want just only strings, you should use `EQUAL` or `EQUALP`.
