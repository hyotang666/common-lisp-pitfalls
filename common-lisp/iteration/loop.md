# Corner cases.
When a non nil atom comes for :ON clause, the `NIL` is returned.
[The specification says](http://www.lispworks.com/documentation/lw51/CLHS/Body/06_abac.htm)

> It checks for the end of the list as if by using atom.

```lisp
(loop :for a :on 'non-nil-atom :collect a) => NIL
```

# Explicitly undefined.
[The specification says](http://www.lispworks.com/documentation/HyperSpec/Body/06_ac.htm)

> If the maximize or minimize clause is never executed, the accumulated value is unspecified. 

```lisp
(loop :for i :in () :minimize i) => unspecified. NIL or 0.
```

# Implementation has its own extension.
[The specification specify loop macro syntax is](http://www.lispworks.com/documentation/HyperSpec/Body/m_loop.htm)

> loop [name-clause] {variable-clause}\* {main-clause}\* => result\*

So the variable clause after the termination test is invalid.
It works in many implementations but not guaranteed especially in clisp.

```lisp
(loop :for i :in '(1 1 1 #\1)
      :while (integerp i)
      :for c = (code-char i) ; <--- invalid.
      :do ...)
```
