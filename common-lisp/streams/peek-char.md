# Ambiguous specification.
[CLHS says](http://www.lispworks.com/documentation/HyperSpec/Body/f_peek_c.htm)

> Exceptional Situations:
> 
> If eof-error-p is true and an end of file[2] occurs an error of type end-of-file is signaled.
> 
> If peek-type is a character, an end of file[2] occurs, and eof-error-p is true, an error of type end-of-file is signaled.
> 
> If recursive-p is true and an end of file[2] occurs, an error of type end-of-file is signaled. 

But there is no sentence about the case of if eof-error-p is `NIL` and end of file occurs and recuesive-p is true.

Implementation may return `NIL`, otherwise signals an error of type `end-of-file`.
At least cmucl signals an error.

```lisp
(with-input-from-string (in "")
  (peek-char t in nil nil t))
#+many-impls
NIL
#+cmucl
Error of type end-of-file
```
