# Implicitly undefined.

Even if it is `SETF`able, no guarantee to `FDEFINITION` returns a function.

```lisp
(defstruct foo bar)
=> FOO

(fdefinition '(setf foo-bar)) => unspecified.

(fdefinition '(setf car)) => unspecified.
```
