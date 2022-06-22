# Explicitly implementation dependent.
[CLHS][character-names] says must support `#\Newline` and `#\Space` only.
And `#\Rubout`, `#\Page`, `#\Tab`, `#\Backspace`, `#\Return`, and `#\Linefeed` are 'semi-standard'.

`#\null` is not standard nor semi-standard.

```lisp
* #\null ; <--- REPL input.

#+(or sbcl ecl)
#\Nul

#+(or ccl clisp cmucl abcl)
#\Null

#+(or allegro)
#\null
```

<!-- Links -->
[character-names]:http://clhs.lisp.se/Body/13_ag.htm
