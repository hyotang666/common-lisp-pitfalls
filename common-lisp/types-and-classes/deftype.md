# Implementation has its own extensions.
[The specifiction says](http://www.lispworks.com/documentation/HyperSpec/Body/m_deftp.htm)

> Recursive expansion of the type specifier returned as the expansion must terminate, including the expansion of type specifiers which are nested within the expansion. 

E.g. clisp works fine.

```lisp
(deftype strings()
  (or null (cons string strings)))
=> STRINGS

(typep :hoge strings)
#+clisp
=> NIL  ; <--- works.
#-clisp
=> infinite expansion.
```
