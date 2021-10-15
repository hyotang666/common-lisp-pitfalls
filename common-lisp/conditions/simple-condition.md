# Implicitly undefined.
Some implementation automatically wraps format control with pprint-logical-block.

```lisp
#+many-impls
(simple-condition-format-control (make-condition 'simple-condition :format-control ""))
=> ""

#+allegro
(simple-condition-format-control (make-condition 'simple-condition :format-control ""))
=> "~1@<~:@>"
```
