# Not in documentation.
When adding the methods for snooze generic-functions (e.g. `snooze:explain-condition`, `snooze:uri-to-arguments` etc.)
such code must be after `defroute` or `defresource` form.

To add methods, you need to specialize method signature e.g. `(r (eql #'your-resource))`.
This `#'` form is evaluated in compile-time and signals an error about an undefined function.
