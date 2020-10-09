# Implicitly undefined.

It is not portable that how to print symbol which has escaped character.

```lisp
\#hoge
=> |#HOGE|
; otherwise
=> \#HOGE
```
