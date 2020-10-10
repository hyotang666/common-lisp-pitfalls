# Not documented.
If you print wide-character rather than ASCII characters, you must set-locale before compiling cl-charms.

To do it, you can use [cl-setlocale](https://github.com/shamazmazum/cl-setlocale).

This is not a good manner but adding a new method is an easy way.

```lisp
(defsystem "your-project"
  :depends-on
  (
   "cl-setlocale"
   ; "cl-charms" ; comment out.
   )
  ...)

;; To set locale just after loading cl-setlocale.
(defmethod perform :after ((o load-op) (c (eql (find-system "cl-setlocale"))))
  (symbol-call "CL-SETLOCALE" "SET-ALL-TO-NATIVE"))

;; To specify loading cl-charms after loading cl-setlocale.
(defmethod component-depends-on ((o load-op) (c (eql (find-system "cl-setlocale"))))
  (append (call-next-method) '((load-op "cl-charms"))))
```
