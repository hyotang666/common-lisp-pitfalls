# ECL violates specification.
[ECL does not support cons type specifier enough.](https://gitlab.com/embeddable-common-lisp/ecl/-/issues/520).
So the code like below will not work in ecl.

```lisp
(typep x '(cons symbol (cons * null)))
```

For maximum portability, you should not use `typep`.
You should write like below.

```lisp
(and (consp x)
     (symbolp (car x))
     (consp (cdr x))
     (null (cddr x)))
```
