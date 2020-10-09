# Implicitly undefined.
ANSI does not say about the error for the second argument `STREAM`.
Many implementations are signaling an error of type `TYPE-ERROR` when the second argument is not input stream, but it is not guaranteed behavior.

E.g. CCL returns 0 successfully when the first argument is an empty sequence.

```lisp
#+ccl
? (read-sequence #() :not-stream)
=> 0
```

Usually, such stupid codes are never written but when you write test code which proves "Signals an error when the parameter is not a stream." you may meet this.
