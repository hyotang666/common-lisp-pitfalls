# Explicitly undefined.
The documentation says

> The consequences are undefined if a namespace is redefined in an incompatible way with the previous one.

Actual behavior is doing nothing. (i.e. like `cl:defvar`.)

If you want to redefine namespace, you need to clean up beforehand.
In a such case, the helper function below may help you.

```lisp
(defun cleanup-namespace (name)
  (let* ((namespace (in-nomine:symbol-namespace name))
         (accessor (in-nomine:namespace-accessor namespace))
         (makunbound-symbol (in-nomine:namespace-makunbound-symbol namespace))
         (boundp-symbol (in-nomine:namespace-boundp-symbol namespace))
         (binding-table-var (in-nomine:namespace-binding-table-var namespace))
         (documentation-table-var
          (in-nomine:namespace-documentation-table-var namespace)))
    (flet ((unbound (name)
             (and name (fmakunbound name))))
      (unbound accessor)
      (unbound makunbound-symbol)
      (unbound boundp-symbol)
      (and binding-table-var (makunbound binding-table-var))
      (and documentation-table-var (makunbound documentation-table-var))
      (in-nomine:namespace-makunbound name))))
```
