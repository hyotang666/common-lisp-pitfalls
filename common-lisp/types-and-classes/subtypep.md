# Implicitly undifined.
Cons type specifier may not subtype of list.

```lisp
#+ECL
(subtypep '(cons (member quote)) 'list) => NIL

#+(or SBCL CLISP CCL)
(subtypep '(cons (member quote)) 'list) => T
```

# Explicitly implmenetation dependent.

[CLHS says][subtypep]

> subtypep is permitted to return the values false and false only when at least one argument involves one of these type specifiers: and, eql, the list form of function, member, not, or, satisfies, or values.


<!-- Links -->
[subtypep]:http://clhs.lisp.se/Body/f_subtpp.htm
[derived type]:http://clhs.lisp.se/Body/26_glo_d.htm#derived_type
