# Difficult to understand.

Symbol `NIL` is also the name of a type.
The `NIL` as type name means empty type.

The type `NIL` is a subtype of every type.

```lisp
(subtypep nil nil) => T
```

Additionally, no object is of type nil.

```lisp
(typep nil nil) => NIL
```

The type containing the object nil is the type null

```lisp
(typep nil 'null) => T
```

Typically I fall in pitfalls like below.

```lisp
(typep '(0) '(cons (eql 0) nil)) => NIL
```
It is `(cons (eql 0) null)` is the correct.

```lisp
(typep '(0) '(cons (eql 0) null)) => T
```
