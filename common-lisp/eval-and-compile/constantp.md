# Difficult to understand.
`CONSTANTP` possibly expands the argument when it is a macro form.
[Specification says](http://www.lispworks.com/documentation/HyperSpec/Body/f_consta.htm)

> If an implementation chooses to make use of the environment information, such actions as expanding macros or performing function inlining are permitted to be used, but not required

If the macro form has a lambda list keyword `&WHOLE` and returns it, the infinite expansion will occur.
To avoid it, you must bind `*MACROEXPAND-HOOK*` with a function which does `GO`, `RETURN-FROM`, or `THROW`.
