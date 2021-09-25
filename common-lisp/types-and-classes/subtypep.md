# Implicitly undifined.
Cons type specifier may not subtype of list.

```lisp
#+ECL
(subtypep '(cons (member quote)) 'list) => NIL

#+(or SBCL CLISP CCL)
(subtypep '(cons (member quote)) 'list) => T
```
