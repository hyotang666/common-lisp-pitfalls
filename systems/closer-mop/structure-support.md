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

If you want to add the method `slot-definition-name`, [this snippet] may be the reference.

[this snippet]: https://github.com/hyotang666/jingoh/commit/f80c156e20bb0fd97e37cf0e19f0e6a7138e5d20#diff-83a539f0f9ea3366d52f60c755028cb124a490a023ab5b171d2caf29dad0af3eR31-R69
