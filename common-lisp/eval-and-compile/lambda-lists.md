# Difficult to understand.
When you specify the keyword parameter, you can use keyword-name as an external keyword.
[The specification says](http://clhs.lisp.se/Body/03_da.htm)

> lambda-list::= (var\*
>                 [&optional {var | (var [init-form [supplied-p-parameter]])}\*]
>                 [&rest var]
>                 [&key {var | ({var | (keyword-name var)} [init-form [supplied-p-parameter]])}* [&allow-other-keys]]
>                 [&aux {var | (var [init-form])}*])

`keyword-name` should be type of `KEYWORD`.
Unfortunately any symbols are accepted but in such case the behavior is unexpected one.

```lisp
;; Good.
(defun test (&key ((:stream *standard-output*) *standard-output*))
  ...)

;; Not good.
(defun test2 (&Key ((modules *modules*) *modules*))
  ...)

* (test2 :modules ()) => Error. No such keywords are supported.

* (test2 'modules ()) => Works.

* (in-package :other)

* (package:test2 'modules ()) => Error. No such keywords are supported.

* (package:test2 'package::modules ()) => Works.
```
