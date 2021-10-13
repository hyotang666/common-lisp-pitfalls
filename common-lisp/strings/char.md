# Corner case.
Referring to the index 0 of empty string signals an error.
It is usual behavior but you can easily forget about it especially to check the first character of the symbol name.

In such a case, `UIOP:STRING-PREFIX-P` can be used.

```lisp
* (char (symbol-name sym) 0) => May error in case when sym is '||.

* (uiop:string-prefix-p #\a sym) ;; Good.
```

