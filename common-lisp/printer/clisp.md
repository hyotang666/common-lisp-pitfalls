# Implementation violates the standard.
[CLISP says]

> The Lisp Pretty Printer implementation is not perfect yet.

## pprint-newline :mandatory does not work.

```lisp
(format nil "~<~:@_~:>" nil) => ""
```

## Nested pprint logical block works incorrect.

```lisp
(with-output-to-string (s)
  (pprint-logical-block (s nil)
    (pprint-logical-block (s nil)
      (format s "~VA" 3 'foo))))
=> " FOO"
```

<!-- Links -->
[CLISP says]:https://www.gnu.org/software/clisp/impnotes.html#clpp
