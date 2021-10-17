# Implicitly undefined.
Readtable may have macro-function for standard alphabet characters.

```lisp
(get-macro-character #\a) => NIL or FUNCTION
```

At least cmucl and allegro have the function `READ-TOKEN`.

If you want to `NIL` for such characters rather than the default function,
you can use `named-readtables::%get-macro-character`.

```lisp
#+(or cmucl allegro)
(named-readtables::%get-macro-character #\a *readtable*)
=> NIL
```

Becare `%get-macro-character`'s second argument is required. (in case of `cl:get-macro-character` is optional.)
Additionaly, `%get-macro-character` does not return secondary value.
