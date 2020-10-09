# Implicitly undefined.
`AND` does not guarantee from left to right order as a type specifier.

```lisp
(typep :hoge '(and integer (satisfies evenp)))
=> unspecified. Works or signals error.
```

For example, [SBCL says](http://www.sbcl.org/manual/#Precise-Type-Checking)

> it is as though all the types were intersected producing a single and type specifier. 
