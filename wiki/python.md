* [The Hitchhiker’s Guide to Python](http://docs.python-guide.org/en/latest/)
* Testing tools: https://wiki.python.org/moin/PythonTestingToolsTaxonomy
  * Branch coverage: [Instrumental](http://instrumental.readthedocs.org/en/latest/index.html)
  * [testfixtures](https://pypi.python.org/pypi/testfixtures)
* Compute a property lazily and only once: http://pypi.python.org/pypi/lazy
* Profiling in production
 * [statprof](https://pypi.python.org/pypi/statprof/) - profiling via statistical sampling
 * [Python Low-Overhead Profiler](https://github.com/bdarnell/plop)
* [Vulture - dead code finder](http://pypi.python.org/pypi/vulture)
* https://pypi.python.org/pypi/caniusepython3
* [GvR explains Twisted Deferreds](https://groups.google.com/forum/#!topic/python-tulip/ut4vTG-08k8/discussion)

To disable nose and pylint simultaneously:
```py
some_line_of_code()  # pragma: nocover # pylint: disable=F0401,W0612
```
