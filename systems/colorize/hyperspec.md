# Not documented.

To enable hyperspec lookup, you need to install hyperspec to your local storage beforehand.

```lisp
sudo apt install hyperspec
```

Then, you need to setf some symbols.

```lisp
(setf clhs-lookup::*hyperspec-pathname* #P"/path/to/hyperspec/root/directory/"
      clhs-lookup::*hyperspec-map-file*
        (merge-pathnames "Data/Map_Sym.txt"
	                 clhs-lookup::*hyperspec-pathname*))
```
