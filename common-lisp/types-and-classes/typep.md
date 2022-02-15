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

# Allegro violates specification.
To test non-NIL atom, you should use `NULL` rather than `LIST`.
Interpreted code works fine, but compiled code.

```lisp
#+allegro
;; Case using LIST.

CL-USER(0): (lambda (x) (typep x '(and atom (not LIST)))) ; <---
#<Interpreted Function (unnamed) @ #x2255447a>

CHECK-BNF(1): (funcall * nil)
NIL ; <--- FINE!

CL-USER(2): (compile nil **)
#<Function (:ANONYMOUS-LAMBDA 69) @ #x22557032>
NIL
NIL

CL-USER(3): (funcall * nil)
T ; <--- WTF!?

;; Case using NULL.

CL-USER(0): (lambda (x) (typep x '(and atom (not NULL)))) ; <---
#<Interpreted Function (unnamed) @ #x2255447a>

CHECK-BNF(1): (funcall * nil)
NIL ; <--- FINE!

CL-USER(2): (compile nil **)
#<Function (:ANONYMOUS-LAMBDA 69) @ #x22557032>
NIL
NIL

CL-USER(3): (funcall * nil)
NIL ; <--- FINE!
```
