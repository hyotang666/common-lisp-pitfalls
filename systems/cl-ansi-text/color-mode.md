# Color does not print.
The default `*COLOR-MODE*` is `:3BIT`.
In such mode, some colors are not printed.
You can use `:8BIT` or `:24BIT` for it.

```lisp
;; Bad example.
(cl-ansi-text:with-color (cl-colors2:+violet+)
  (princ :hoge))

;; Works fine!
(let ((cl-ansi-text:*color-mode* :8bit))
  (cl-ansi-text:with-color (cl-colors2:+violet+)
    (princ :hoge))
```

