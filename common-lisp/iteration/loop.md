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

# Implicitly undefined. (?)
I could not find an article about for-as-across subclause uses `AREF`.

This means when vector has fill-pointer, `LOOP` may iterate inactive region.

# Difficult to understand.
## INITIALLY clauses can not refer for-as-equals-then subclause.
`:INITIALLY` clauses are evaluated in the loop prologue.

[CLHS says](http://www.lispworks.com/documentation/HyperSpec/Body/06_agb.htm)

> The initially construct causes the supplied compound-forms to be evaluated in the loop prologue, which precedes all loop code except for initial settings supplied by constructs with, for, or as.

`for-as-equals-then` subclauses are initialized on the first iteration.

[CLHS says](http://www.lispworks.com/documentation/HyperSpec/Body/06_abad.htm)

> In the for-as-equals-then subclause the for or as construct initializes the variable var by setting it to the result of evaluating form1 on the first iteration

Consequently, in the `:INITIALLY` clause forms, for-as-equals-then subclauses are not referred to since such variables are set on the iteration body (more correctly, you can refer to it but its value is NIL).
