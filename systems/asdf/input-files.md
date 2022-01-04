# Not documented. Corner case.
`asdf:input-files` is memoized. (At least version 3.3.5.)
If you want to control return values, you need another object.

I have got this issue when I implemented asdf support for [cl-yesql].
Snippet is [here].

[cl-yesql]:https://github.com/ruricolist/cl-yesql
[here]:https://gist.github.com/hyotang666/e54d4be187a9485a67dd24fc6f6a3dbf
