# Implicitly undefined.
Output binary data to the stream that is returned by `(make-broadcast-stream)` may signal an error.

[CLHS says]

> (If a broadcast stream has no component streams, then all output to the broadcast stream is discarded.)

also says

> if there are no component streams, file-length and file-position return 0, file-string-length returns 1, and stream-external-format returns :default.

Many implementations accept binary data for it, but at least cmucl signals an error.

For maximum portability, `uiop:null-device-pathname` may help you.

```lisp
(with-open-file (out (uiop:null-device-pathname) :direction :output
                     :if-exists :append :element-type '(unsigned-byte 8))
  (write-byte 8 out))
```

NOTE: Both `uiop:with-null-output` and `uiop:call-with-null-output` depends on `(make-broadcast-stream)`.
So you can not use it with binary data at least in cmucl.

<!-- Links -->
[CLHS says]:http://www.lispworks.com/documentation/HyperSpec/Body/t_broadc.htm#broadcast-stream
