# Difficult to understand.

[The specification says](http://www.lispworks.com/documentation/HyperSpec/Body/v_debug_.htm)

> The initial value might also be a generalized synonym stream to either the symbol *terminal-io* or to the stream that is its value. 

In many implementations, for example, binds `*STANDARD-OUTPUT*` with `*STANDARD-INPUT*` signals an error, but it is not guaranteed.
E.g. CCL works.

```lisp
#+ccl
(output-stream-p *standard-input*) => T
```

Usually, such stupid codes are never written but when you write test codes that check "Signals an error when the function which expects output stream gets input-stream" such test may be successful unexpected.

# Corner case.
[CLHS says](http://www.lispworks.com/documentation/HyperSpec/Body/26_glo_s.htm#stream_variable_designator)

> stream variable designator n. a designator for a stream variable; that is, a symbol that denotes a stream variable and that is one of: t (denoting *terminal-io*), nil (denoting *standard-input* for input stream variable designators or denoting *standard-output* for output stream variable designators), or some other symbol (denoting itself). 

`NIL` is a valid stream designator but it does not mean that it fits for `*STANDARD-INPUT*` nor `*STANDARD-OUTPUT*`.
Ordinary you may not bind (e.g.) `*STANDARD-INPUT*` by `NIL`, but when defining the function that accepts `IF-EXISTS` parameter for `OPEN` unexpectedly do it.

```lisp
;; Bad example.
(defun save-file (name &optional if-exists)
  (with-open-file (*standard-output* ; <--- May signal an error due to NIL is not a STREAM.
                    :direction :output
                    :if-exists if-exists
                    :if-does-not-exist :create)
    (write :hoge)))

;; Good example.
(defun save-file (name &optional if-exists)
  (with-open-file (out
                    :direction :output
                    :if-exists if-exists
                    :if-does-not-exist :create)
    (write :hoge :stream out)))
```
