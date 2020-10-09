# Explicitly undefined.

Backquote is implementation-dependent.
Many implementations generate a macro form which generates codes in macro expansion time, but some implementations are designed to be implemented as reader macro that generates codes in read-time.

```lisp
'`(hoge ,@(cdr '(1 2 3))) => implementation-dependent.
                          ; `(HOGE ,`(CDR '(1 2 3))) in many impls.
                          ; (LIST* 'HOGE (CDR '(1 2 3))) in CCL.
```

What you want may [fare-quasiquote](https://gitlab.common-lisp.net/frideau/fare-quasiquote).

