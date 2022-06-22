# Implicitly undefined.
Calling `READ` as toplevel with specifying recursive-p is non-NIL is undefined.

[CLHS says][]

>  If recursive-p is supplied and not nil, it specifies that this function call is not an outermost call to read but an embedded call, typically from a reader macro function. It is important to distinguish such recursive calls for three reasons.
> 
> 1. An outermost call establishes the context within which the #n= and #n# syntax is scoped.

but I could not find the sentence about the case of calling the `READ` as toplevel with specifying recursive-p is non-NIL.

The implementation may read the form which uses read-time-labeling successfully or may not.

```lisp
;; The implementation that signals an error before read actually.
#+(or sbcl)
* (read nil t t t)
; ERROR

;; The implementation that signals an error at read actually.
#+(or clisp cmucl)
* (read nil t t t)
(#0=1 #0#) ; <--- User input.
; ERROR

;; The implementation that read labelled form successfully.
#+(or ccl ecl allegro abcl)
* (read nil t t t)
(#0=1 #0#) ; <--- User input.

(1 1)
```
