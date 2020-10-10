# Implicitly undefined, Ambiguous specification.

[The specification says](http://www.lispworks.com/documentation/HyperSpec/Body/09_ac.htm)

> When a condition is printed and \*print-escape\* is false, the condition reporter for the condition is invoked.

and [report message is defined as](http://www.lispworks.com/documentation/HyperSpec/Body/26_glo_r.htm#report_message)

> the text that is output by a condition reporter. 

So any text is report message of course it includes an abbreviated fashion according to the style of the implementation (e.g., by print-unreadable-object).

```lisp
(princ (nth-value 1 (ignore-errors (/ 2 0))))
=> unspecified. Division by zero. or #<DIVISION-BY-ZERO #X123456>
```
