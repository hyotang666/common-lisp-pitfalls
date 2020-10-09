# Implicitly undefined.

In many implementations, you can not print the list `(FUNCTION HOGE)`.
It will be `#'HOGE`.
I could not find how to do it in CLISP, ECL, CCL.

SBCL can do it.

```lisp
#+sbcl
(write '(function hoge) :pretty nil)
(FUNCTION HOGE) ; <--- outout.
#'HOGE          ; <--- return value.

#-sbcl
(write '(function hoge) :pretty nil)
#'HOGE          ; <--- output.
#'HOGE          ; <--- return value.
```

Samely you can not print the list `(QUOTE HOGE)`.
