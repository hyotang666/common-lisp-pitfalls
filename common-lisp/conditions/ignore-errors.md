# Corner cases.

Macro `IGNORE-ERRORS` returns `(VALUES NULL CONDITION)` when capturing the signaled condition.
If the form does not signal a condition, returns the returned value of the form.

When you bind such values with `MULTIPLE-VALUE-BIND` and check the second value you will confuse second values that are successfully returned or not.
To avoid it, you should use `HANDLER-CASE` rather than `IGNORE-ERRORS`.

```lisp
(handler-case (values :a (make-condition 'error))
  (error (c) c)
  (:no-error (&rest values)
    (values-list values)))
=> :A, #<ERROR {...}>
```
