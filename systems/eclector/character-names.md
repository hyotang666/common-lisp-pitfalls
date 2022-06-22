# Explicitly unsupported.
[Eclector says][find-character]

> A default method on this generic function that is not specialized to any particular client but is specialized to designator being a string recognizes the mandatory character names listing in HyperSpec Section 13.1.7 Character Names. Another default method on this generic function that is not specialized to any particular client but is specialized to designator being a character just returns designator. 

```lisp
(eclector.reader:read-from-string "#\null") => ERROR
```

<!-- Links -->
[find-character]:https://s-expressionists.github.io/Eclector/eclector.html#index-find_002dcharacter-_005beclector_002ereader_005d
