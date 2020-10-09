# Difficult to understand.

When you want to specify `T` or `NIL` as the clause keys, you must list it otherwise `NIL` is interpreted as empty clause keys, and `T` is interpreted as a default clause.

```lisp
(case var
  (nil :this-clause-is-never-chosen.)
  ((nil) :ok.)
  (t :this-clause-is-treated-as-default-clause.)
  ((t) :ok.))
```
