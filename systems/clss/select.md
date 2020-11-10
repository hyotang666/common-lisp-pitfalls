# Undocumented pitfalls.
Sometimes you got `SELECT` fails to select the correct DOM.
It may `PLUMP-DOM` the reason.

[`PLUMP`](https://github.com/Shinmera/plump) makes `TEXT-NODE` for text between tags even if the text is just for indentation.
In such cases `CLSS:SELECT` can not select the correct DOM unless doing `PLUMP:STRIP`.

`PLUMP:STRIP` removes any nodes that have empty strings.

```lisp
* (defvar root (plump:parse "<td>
                               <div></div>
                               <center></center>
                             <td>"))
ROOT

* (clss:select "div+center" root)
#()

* (plump:next-sibling (aref (clss:select "div" root) 0))
#<PLUMP-DOM:TEXT-NODE {...}>

* (plump:text *)
""

* (clss:select "div+center" (plump:strip root))
#(#<PLUMP-DOM:ELEMENT center {...}>)
```
