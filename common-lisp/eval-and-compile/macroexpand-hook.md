# Difficult to understand.
The API of the function that is the variable `*MACROEXPAND-HOOK*` should be bound by is `(expander form env)`.
In such functions, doing something then do `FUNCALL` the macro-function `expander` with `form` and `env`.

[CLHS shows the example like below.](http://clhs.lisp.se/Body/v_mexp_h.htm)

> (defun hook (expander form env)
>    (format t "Now expanding: ~S~%" form)
>    (funcall expander form env)) =>  HOOK 
> (defmacro machook (x y) `(/ (+ ,x ,y) 2)) =>  MACHOOK 
> (macroexpand '(machook 1 2)) =>  (/ (+ 1 2) 2), true 
> (let ((*macroexpand-hook* #'hook)) (macroexpand '(machook 1 2)))
> >>  Now expanding (MACHOOK 1 2) 
> =>  (/ (+ 1 2) 2), true

NOTE! : In the code above, the function `HOOK` shadows the outer `*MACROEXPAND-HOOK*` function.
So the outer hook function never called.
To avoid it, you should write like below.

```lisp
(defun hooker (outer-hook)
  (lambda (expander form env)
    ...
    (funcall outer-hook expander form env)))

(let ((*macroexpand-hook* (hooker *macroexpand-hook*)))
  ...)
```

The function `HOOKER` returns the function which encloses the outer `*MACROEXPAND-HOOK*` function.

`*MACROEXPAND-HOOK*` can not refer outer `*MACROEXPAND-HOOK*` since it is a special variable that binds dynamically.
If you do it, infinite recursion occurs.
