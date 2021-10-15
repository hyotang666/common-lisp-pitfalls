# Ambiguous specification (?), Implementation violates specification (?)
Some implementation silently ignore third element in the binding.

```lisp
#+many-impl
(let ((var :init-form :too-much)) var) => Error

#+allegro
(let ((var :init-form :too-much)) var) => :INIT-FORM
```
