# Ambiguous specification.

[The specification says](http://www.lispworks.com/documentation/HyperSpec/Body/f_list_.htm)

> list\* &rest objects+ => result

but also says

> Exceptional Situations: None. 

When you call `LIST*` with no arguments, the result is not guaranteed.

```lisp
#+(or clisp sbcl ccl)
(list*) => ERROR

#+ecl
(list*) => NIL
```
