Ansi does not say about error for second argument `STREAM`.
Many impls are signaling an error of type `TYPE-ERROR` when the second argument is not input stream, but it is not guaranteed behavior.

e.g. CCL return 0 successfully when the first argument is empty sequence.

```lisp
#+ccl
? (read-sequence #() :not-stream)
=> 0
```

Usually such stupid codes are never written but when you write test code which proves "Signals an error when parameter is not stream." you may meet this.
