# Implementation has its own extensions.

[The specification says `PATHNAME` API is](http://www.lispworks.com/documentation/HyperSpec/Body/f_pn.htm)

> pathname pathspec => pathname

and pathspec is

> pathspec---a pathname designator. 

[and pathname-designator is](http://www.lispworks.com/documentation/HyperSpec/Body/26_glo_p.htm#pathname_designator)

>  one of: a pathname namestring (denoting the corresponding pathname), a stream associated with a file (denoting the pathname used to open the file; this may be, but is not required to be, the actual name of the file), or a pathname (denoting itself). 

but there are the implementations that accept symbol as pathname-designator.

```lisp
(pathname :/foo/bar/bazz) => #P"/foo/bar/bazz" ; Error in spec.
```
