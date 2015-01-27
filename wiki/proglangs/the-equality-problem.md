`"hello".equals(42)` should be a compile-time type error

Also, given:
* `non-abstract class Circle(int radius)`
* `non-abstract class ColoredCircle(int radius, Color color) extends Circle(int radius)`

Then: `somePlainCircle == someColoredCircle` should probably be a type error.

What is the color of a colorless circle? What color could an undefined color possibly be equal to?
