# Implicitly undefined. Ambiguous specification.
Multi time read and unread character is not guaranteed (?).

```lisp
(with-input-from-string (in "abcd")
  (let ((a (read-char in)))
    (let ((b (read-char in)))
      (unread-char b in)
      (unread-char a in)))
  (read-char in))
```
Above code successfully return `#\a` at least sbcl, ecl, ccl.
But clisp signals an error.

[CLHS says](http://clhs.lisp.se/Body/f_unrd_c.htm)

> Notes:
> 
> unread-char is intended to be an efficient mechanism for allowing the Lisp reader and other parsers to perform one-character lookahead in input-stream. 
