# Diffucult to understand.

If the macro function has a lambda list keyword `&WHOLE` and returns it, the second return values become `T` even if it is not expanded.

[The specification says](http://www.lispworks.com/documentation/HyperSpec/Body/f_mexp_.htm)

> If form is a macro form, then the expansion is a macro expansion and expanded-p is true.

So `MACROEXPAND` will get into infinite expansion.
To avoid it, you must bind `*MACROEXPAND-HOOK*` with a function that does `GO`, `RETURN-FROM`, or `THROW`.
