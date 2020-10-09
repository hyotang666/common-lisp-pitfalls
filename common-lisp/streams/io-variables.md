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
