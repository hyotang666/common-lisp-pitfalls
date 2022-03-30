# Difficult to understand.
Declaration scope includes update-form, end-test-form and finally-forms.

If you want to declare for only loop body forms, you need to use `locally`.

```lisp
;; Bad example due to VAR bound by NIL finally.
(do ((var '(1 2 3)) (cdr var))
  ((null var) :done)
  (declare (fixnum var))
  (print var))
  
;; To make scope narrow.
(do ((var '(1 2 3) (cdr var)))
  ((null var) :done)
  (locally ; <--- This!
    (declare (fixnum var))
    (print var)))
```
