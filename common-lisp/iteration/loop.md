# Corner cases.
When a non nil atom comes for :ON clause, the `NIL` is returned.
[The specification says](http://www.lispworks.com/documentation/lw51/CLHS/Body/06_abac.htm)

> It checks for the end of the list as if by using atom.

```lisp
(loop :for a :on 'non-nil-atom :collect a) => NIL
```
