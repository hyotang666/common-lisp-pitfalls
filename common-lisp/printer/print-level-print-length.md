# Ambiguous specification. Implicitly undefined.

There are some interpretations about `*PRINT-LENGTH*` of `STRUCTURE` object.

CLISP seems to interpret structure as an atom.
CCL seems to interpret every elements is the element includes structure name and slot names.
SBCL and ECL seem to interpret the pair of slot name and slot value is the one element and ignore type name.

```lisp
(defstruct foo a b c d)
=> FOO

(let ((*print-length* 2))
  (print (make-foo :a (list 1 2 3 4 5))))

#+clisp
#S(FOO :A (1 2 ...) :B NIL :C NIL :D NIL)

#+ccl
#S(FOO :A ...)

#+(or sbcl ecl)
#S(FOO :A (1 2 ...) :B NIL ...)
```
