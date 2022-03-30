# Difficult to understand.
Keyword argument `:FROM-END` works reverse order.

```lisp
* (position 0 '(0 0 0)) => 0
* (position 0 '(0 0 0) :from-end t) => 2
```

And this means from **end**, not from last element.

```lisp
* (position 0 '(0 0 0) :from-end t :end 1) => 0
```

Keyword argument `:START` and `:END` specifies left most region (inclusive) and right most region (exclusive) respectively.

```lisp
* (position 0 (alexandria:iota 31) :start 13 :end 27 :from-end t)

;;                               |> :start (inclusive)
;;                               |                           :end (exclusive) <|
;; (0 1 2 3 4 5 6 7 8 9 10 11 12 | 13 14 15 16 17 18 19 | 20 21 22 23 24 25 26 | 27 28 29 30)
;;                               |                                         <---| :from-end starts from here.
;;  :from-end ends to here. ---> |
```
