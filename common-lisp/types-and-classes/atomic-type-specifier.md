# Implementation violates the standard.
[CLHS says][atomic-type-specifier]

> For every atomic type specifier, x, there is an equivalent compound type specifier with no arguments supplied, (x). 

But many implementations (e.g. at least sbcl, ccl, ecl, clisp, allegro, and cmucl) violate it.

I think the compound type specifier like `(list #|of string|#)` is useful for the documentation but unfortunately, such code does not work.

If you really want it, [trivial-types] might help you.

<!-- Links -->
[atomic-type-specifier]:http://www.lispworks.com/documentation/HyperSpec/Body/26_glo_a.htm#atomic_type_specifier
[trivial-types]:https://github.com/m2ym/trivial-types
