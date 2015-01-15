* Compute a property lazily and only once: http://pypi.python.org/pypi/lazy

To disable nose and pylint simultaneously:
```py
some_line_of_code()  # pragma: nocover # pylint: disable=F0401,W0612
```
