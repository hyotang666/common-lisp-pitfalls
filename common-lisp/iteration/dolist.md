# Difficult to understand.
[CLHS say](http://clhs.lisp.se/Body/m_dolist.htm)

> At the time result-form is processed, var is bound to nil.

and also

> The scope of the binding of var does not include the list-form, but the result-form is included.

so, type declaration about binding is needed to care about `NIL` case.

```lisp
;; Invalid since var STRING bound by NIL in result form.
(dolist (string '("a" "b" "c"))
  (declare (string string))
  ...)

;; Valid
(dolist (string '("a" "b" "c"))
  (declare ((or null string) string))
  ...)
```

It may be a `LOOP` macro that you want.

```lisp
(loop :for string :of-type string :in '("a" "b" "c")
      :do ...)
```
