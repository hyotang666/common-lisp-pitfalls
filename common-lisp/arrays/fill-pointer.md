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

# Explicitly undefined.
Abount Function REMOVE, REMOVE-IF, REMOVE-IF-NOT, DELETE, DELETE-IF, DELETE-IF-NOT

[CLHS says](http://clhs.lisp.se/Body/f_rm_rm.htm)

> If sequence is a vector, the result might or might not be simple, and might or might not be identical to sequence.

```lisp
#+(or sbcl ccl clisp ecl clasp cmucl)
(array-has-fill-pointer-p (delete 0 (make-array 4 :fill-pointer 2 :initial-element 0)))
=> T

#+(or allegro)
(array-has-fill-pointer-p (delete 0 (make-array 4 :fill-pointer 2 :initial-element 0)))
=> NIL
```

For maximum portability, you should use your own sequence functions like below.

```lisp
(defun delete% (item vector &key (key #'identity))
  (loop :for index :upfrom 0 :below (fill-pointer vector)
        :with fill-pointer = 0
        :unless (eql item (funcall key (aref vector index)))
          :do (setf (aref vector fill-pointer) (aref vector index)) ; shift
              (incf fill-pointer)
        :finally (setf (fill-pointer vector) fill-pointer)
                 (return vector)))
```
