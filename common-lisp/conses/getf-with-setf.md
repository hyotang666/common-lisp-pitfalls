# Explicitly implementation dependent.
[CLHS says](http://clhs.lisp.se/Body/c_conses.htm)

> setf of getf is permitted to either write the value of place itself, or modify of any part, car or cdr, of the list structure held by place. 

[and also say](http://www.lispworks.com/documentation/lw50/CLHS/Body/05_abb.htm)

> * A function call form whose first element is the name of any one of the functions in the next figure, provided that the supplied argument to that function is in turn a place form; in this case the new place has stored back into it the result of applying the supplied ``update'' function.
> 
>     Function name  Argument that is a place  Update function used      
>     ldb            second                    dpb                       
>     mask-field     second                    deposit-field             
>     getf           first                     implementation-dependent  

Note about update function for `FIRST` is implementation-dependent.

[CLHS also say](http://www.lispworks.com/documentation/lw50/CLHS/Body/05_abb.htm)

> (Note that the phrase ``possibly-new property list'' can mean that the former property list is somehow destructively re-used, or it can mean partial or full copying of it. Since either copying or destructive re-use can occur, the treatment of the resultant value for the possibly-new property list must proceed as if it were a different copy needing to be stored back into the generalized variable.) 

When `SETF` is used with `GETF` that refers a variable, it may be a list what is destructed or may be a variable what is destructed. (i.e. superseded.)

```lisp
* (flet ((add (plist)
           (setf (getf plist :key) :exist?)))
    (let ((list (list :a :b)))
      (add list)
      list))
=>
#+(or sbcl ccl ecl allegro cmucl abcl)
(:A :B)

#+(or clisp)
(:KEY :EXIST? :A :B)
```

You will be trapped this pitfall when you define `SETF` function like below.

```lisp
(defun (setf my-function) (new plist)
  (setf (getf plist :key) new))

* (let ((l (list :a :b)))
    (setf (my-function l) :new)
    l)
=> (:A :B)
```

If you want to destruct a list, you should use `NCONC` rather than `SETF` with `GETF`.

```lisp
(defun (setf my-function) (new plist)
  (let ((sentinel '#:sentinel))
    (if (eq sentinel (getf plist :key sentinel))
        (nconc plist (list :key new))
        (setf (getf plist :key) new)))
  new)

* (let ((l (list :a :b)))
    (setf (my-function l) :new)
    l)
=> (:A :B :KEY :NEW)
```
