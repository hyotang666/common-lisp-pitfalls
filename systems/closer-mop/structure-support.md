# Explicitly undefined.
Meta object protocol for structure-class is undefined.

Many implementations (partially) support meta-object-protocol for structure class.

```lisp
(defstruct struct slot)

(mapcar #'c2mop:slot-definition-name (c2mop:class-slots (class-of (make-struct))))
=> (SLOT)
```

But at least ABCL, does not support.

```
#+abcl
(defstruct struct slot)

(mapcar #'c2mop:slot-definition-name (c2mop:class-slots (class-of (make-struct))))
=> Error
```

