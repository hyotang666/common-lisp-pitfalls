# Implementation has its own extensions.
[The specification says](http://www.lispworks.com/documentation/HyperSpec/Body/m_w_in_f.htm)

> string---a form; evaluated to produce a string. 

but ECL accepts string designator.

```lisp
#+ecl
(with-input-from-string(s :hoge)
  (read s))
=> HOGE ; Error in spec.

(with-input-from-string(s #\c)
  (read s))
=> C ; Error in spec.
```
