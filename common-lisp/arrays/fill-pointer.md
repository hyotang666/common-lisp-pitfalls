# Implicitly undefined (?)
[CLtL2 says](https://www.cs.cmu.edu/Groups/AI/html/cltl/clm/node162.html#SECTION002150000000000000000)

> Nearly all functions that operate on the contents of a vector will operate only on the active elements.
> An important exception is aref, which can be used to access any vector element whether in the active region of the vector or not. 

but I could not find such articles in CLHS.

Additionally I could not find `LOOP` macro keyword `ACROSS` uses `AREF` or not.
`LOOP` macro may iterate the inactive region.

To iterate an active element of a vector which has fill-pointer, you should write like below.

```lisp
* (defvar *a* (make-array 10 :fill-pointer 0))
=> *A*

* (vector-push-extend :first *a*)
=> 0

* *a*
=> #(:FIRST)

* (fill-pointer *a*)
=> 1

* (loop :for i :upfrom 0 :below (fill-pointer *a*)
        :collect (aref *a* i))
=> (:FIRST)

;; PITFALLS!
* (loop :for e :across *a* :collect e)
may return (:FIRST 0 0 0 0 0 0 0 0 0)
or         (:FIRST)
```


