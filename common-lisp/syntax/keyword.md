# Explicitly undefined.
The token that has a double colon prefix e.g. `::foo` is [undefined.](http://clhs.lisp.se/Body/02_ce.htm)

```lisp
#+(or sbcl ccl clisp ecl cmucl allegro)
* ::hoge
:HOGE

#+abcl
* ::hoge
:|:HOGE|

#+clasp
* ::hoge

Condition of type: TWO-PACKAGE-MARKERS-MUST-NOT-BE-FIRST
A symbol token must not start with two package markers as in ::name.
Available restarts:
(use :r1 to invoke restart1, etc.)

1. (RECOVER) Treat the character as if it had been escaped.
2. (RESTART-TOPLEVEL) Go back to Top-Level REPL.
```
