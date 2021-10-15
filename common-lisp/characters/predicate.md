# Implicitly undefined.
`CHAR=` or its family may signals an error when its argument is not character.

```lisp
#+(or sbcl ccl ecl clisp)
(char= #\a :not-characer) => Error

#+allegro
(char= #\a :not-character) => NIL
```
