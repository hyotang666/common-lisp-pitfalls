# Implicitly undefined.
[CLHS only says][dispatch-macro]

> If the character is a letter, its case is not important; #O and #o are considered to be equivalent, for example.

The implementations may keep the case or may not keep.

```lisp
* (set-dispatch-macro-character #\# #\j (lambda (in c n) `(list ,(read in t t t) ,c ,n)))
=> Implementation dependent return value.

;; The implementations that converts the dispatch macro character.
#+(or sbcl ccl cmucl)
* #j(+)     ; <--- The down case is
(0 #\J NIL) ; <--- converted to the up case.
* #J(+)
(0 #\J NIL)

;; The implementations that keeps the case of the character.
#+(or clisp ecl allegro abcl)
* #j(+)     ; <--- The down case
(0 #\j NIL) ; <--- is kept.
* #J(+)
(0 #\J NIL)
```

<!-- Links -->
[dispatch-macro]:http://clhs.lisp.se/Body/02_dh.htm
