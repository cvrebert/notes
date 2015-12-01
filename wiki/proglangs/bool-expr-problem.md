Having the traditional boolean operators always return boolean values as results isn't flexible enough.

* Matrix math libraries like NumPy want to make them operate matrix-wise and result in a matrix
* ORM libraries want to use them to formulate query expressions
  * But on an individual row/active-record, we want them to produce a boolean
* The normal short-circuiting behavior of these operators

ORM example:
```scala
class Task(
  val deadline: Timestamp,
  val completedAt: Timestamp
) {
  def isExpired = completedAt >= deadline
}
```

Possible solution: Return some kind of `BooleanExpression` rather than a `Boolean`, which evaluates to a `Boolean` in the context of conditions, but which can be used as an AST in other contexts.
