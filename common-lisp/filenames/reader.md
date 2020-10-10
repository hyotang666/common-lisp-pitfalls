# Explicitly implementation dependent.

Literal #P"" syntax may have `VERSION` information.

```lisp
(pathname-version #P"") => :NEWEST
```

[The specification says](http://www.lispworks.com/documentation/HyperSpec/Body/02_dhn.htm)

> #P<<expression>> is equivalent to #.(parse-namestring '<<expression>>)

and [`PARSE-NAMESTRING` API is](http://www.lispworks.com/documentation/HyperSpec/Body/f_pars_1.htm)

> parse-namestring thing &optional host default-pathname &key start end junk-allowed

and about default-pathname is

> The default is the value of \*default-pathname-defaults\*

and [`*DEFAULT-PATHNAME-DEFAULTS*` is said](http://www.lispworks.com/documentation/HyperSpec/Body/v_defaul.htm)

> An implementation-dependent pathname
