# Difficult to understand.
The ordinary type-specifier specifies the type of the first return value.
It means multiple values are possibly returned.

```lisp
(the integer (values 0 1)) ; <--- ok.
```

When you specify the values type specifier, you can use the `VALUES` type specifier.

```lisp
(the (values integer integer) (values 0 1)) ; <--- ok
```

But in the above case, there is a possibility that the third or more values may be returned.

```lisp
(the (values integer integer) (values 1 2 3)) ; <--- ok
```

If you want to specify return value is just only one, `&OPTIONAL` allows you to do it.

```lisp
(the (values integer &optional) (values 1 :over)) ; <--- not ok.
```
