# Explicitly implementation dependent.
[See](http://www.lispworks.com/documentation/HyperSpec/Body/12_aaaa.htm)

So return type of `(* 0 0.0)` is implementation dependent.

```lisp
(* 0 0.0) => 0 or 0.0
```
