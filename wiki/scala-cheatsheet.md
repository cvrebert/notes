### Environment
* Use `mvn scala:console` to get a Scala REPL with all of your classes & dependencies on the classpath (and thus importable)
* To workaround an annoying bug and not bork your terminal afterwards: `echo 'jline.shutdownhook=true' > ~/.jline.rc`

### Operators
* Func call operator is `apply`
  * defining it on a class' companion object is one way to provide an (alternate) convenience constructor
* No `[]` operator; call a collection like a function instead
* You can assign to function calls; this calls the `update` method
* When an object is immutable, `+=` etc. desugar like in Python
* Unlike in Java, `==` is not retarded, and even handles null
* `x -> y` results in a 2-tuple
* `::` is cons
* `:::` is list concat
* `x +: xs` is immutable prepend
* `xs :+ x` is immutable append
* Prefix operators: `+`, `-`, `!`, `~`
  * invoke `unary_+` etc methods
* any method of 1 argument can be called like infix operator: `foo whateverMethod bar` === `foo.whateverMethod(bar)`
* `foo.bar = baz` can desugar to a call to the `bar_=` method of foo

### For-expression
```scala
// super-simple
for {x <- xs if x.somePredicate} {
    // do something
}
 
// nested iteration, with inline filters
for {
    file <- files
    if file.isText
    line <- file.lines
    trimmed = line.trim // can create inline val for intermediate result
    if trimmed.startswith("//")
} {
    println(trimmed)
}
 
// construct new collection using "yield"
val trimmedLineLengths = for {line <- file.lines} yield { line.trim }
```
* ~~NOTE: Scala does NOT have `break` or `continue`~~

## Strings/Chars
Like Java: single-quotes are for chars, double-quotes are for strings
Has Python-style triple-quoted strings

## Collections
* declare things as `Seq` rather than `List`
* `import scala.collection.JavaConverters._` for non-copying `.asJava` & `.asScala` interconversion methods
* the empty list is `Nil`
* `mkString(sep)` is the string-join-with-separator operation
* for lazy collection computations, use `.iterator`
* `1 to 3` gives 1,2,3
* `1 until 3` gives 1,2
* `Seq(1,2,3,4).sliding(2)` gives `List(1, 2), List(2, 3), List(3, 4)`
* `Seq(1,2).sliding(5)` gives `List(1, 2)`
* `Seq(1,2,3,4,5,6,7).grouped(3)` gives `List(1, 2, 3), List(4, 5, 6), List(7)`
* `Seq('a','b','c').zipWithIndex` gives `(a,0),(b,1),(c,2)`

## Functions
def statements can be nested
Nothing return type indicates throwing an exception (no normal return ever occurs)

```scala
// Varargs
def foo(args: String*) = ...  // declaring
foo(someArray: _*)  // using
 
 
// Currying
def foo(bar: Int)(baz: Int) = ...
 
 
// Anonymous funcs
val myFunc = (x: Int) => x + 42
Seq(1, 2, 3).map { x => x + 1}  // Parameter parens and type can be omitted when the type is inferrable
 
// Call-by-name
object Foo {
    var enableLogging = true
    def efficientLog(message: => String) {  // note lack of "()" in the declaration of the message function argument
        if (enableLogging) {
            println("BEGIN")
            println(message)  // note that the function is called without explicitly calling it
            println("MIDDLE")
            println(message)  // note: the function is called again every time we reference it
            println("END")
        }
    }
    def expensiveComputation = {
        println("Computing...")
        "42"
    }
}
Foo.efficientLog(Foo.expensiveComputation)  // the argument is implicitly wrapped in an anonymous function
/* Output:
BEGIN
Computing...
42
MIDDLE
Computing...
42
END
*/
Foo.enableLogging = false
Foo.efficientLog(Foo.expensiveComputation)  // No output; the argument was never referenced
```

### Imports
```scala
import java.util._  // wildcard import
import train.{Engineer => TrainEngineer}  // renaming import
import java.util.{List,Map,Set}  // import certain named things
```

### Generics
```scala
class ImmutableList[+T](...) {// covariant; (which is typical)
    // ImmutableList[subclass_of_T] can substitute for ImmutableList[T]
    // T cannot be directly used as a method parameter type
    def cons[S >: T] // S must be (superclass of) T
            (item: S): ImmutableList[+S] = new ImmutableList(item, this)
        // Why S must be (superclass of) T:
        //      List[Base] + List[Subclass] => List[Base]; CANNOT make List[Subclass]
        //      List[Base] + List[Superclass] => List[Superclass]; this is why we care about the superclass case
}
 
class PrintableList[T <: Printable] // T must be (subclass of) Printable
 
class Sink[-T] { // contravariant; (which is unusual; basically only for function-like stuff)
    // Sink[superclass_of_T] can substitute for Sink[T]
    def consume(item: T)
    // TeeTo(Sink[Base], Sink[Subclass]) => TeeTo<Subclass>
    // TeeTo(Sink[Base], Sink[Superclass]) => TeeTo<Base>
    // Sink[Superclass] can deal with Subclass instances
}
```

### Pattern Matching
```scala
val result = node match {
    case 0 => 0
    case BinaryOperation(e, "+", 0) => e
    case BinaryOperation(left, "+", right) if left == right => BinaryOperation(2, "*", left)  // can use "if" guards
    case Floor(f@Floor(_)) => f  // i.e. flooring is idempotent
    case s: String => Integer.parse(s)
    case _ => "not defined"
}
 
 
// Making your own non-case classes work with pattern matching:
class CurrencyAmount(val wholePart: Int, val fracPart: Int, val currencyCode: String) {
    // the "unapply" method is used as an "extractor"/"deconstructor" in destructuring binds in pattern matches
    def unapply(String string):  Option[Int, Int, String] = ...  // e.g. it turns "12.34 USD" into (12, 34, "USD")
         
}
object FormattedNumber {
    // If you don't wish to bind any variables, return a Boolean indicating whether the match should succeed
    def unapply(String string): Boolean = string.filter{ c => !(",.0123456789" contains c) }.length > 0
}
object CommaSeparatedList {
    // To bind arbitrarily many things
    def unapplySeq(String str): Option[Seq[String]] = str.split(",")
}
// Using it:
someString match {
    case CurrencyAmount(whole, fractional, currency) => println("Valid currency amount denominated in " + currency)
    case FormattedNumber => println("Plausible number")
    case CommaSeparatedList("a", "b", "c") => println("You entered: a,b,c")
    case _ => println("Invalid input!")
}
```

### Misc
* no checked exceptions (smile)
* Scala performs tail-call optimization (TCO) on final self-recursive methods; use @tailrec to ensure your method is written correctly
* `throw` can be used in an expression context; same semantics as usual
* `try-catch` is an expression
```scala
// try-catch uses pattern matching
try {
    val f = new FileReader("foo.txt")
}
catch {
    case ex: FileNotFoundException => handleTheException
    case ex: IOException => handleTheException
}
```

### Classes
* default access level is public
* filenames need not correspond to class names
* package can be used as a block-scoped construct

```scala
class Rational(val numer: Int, val denom: Int) \
    extends Integral(superklass, constructorArgs, goHere) \ // superclass
    with AlgebraicField with Mathematical { // mix-in some traits
    // these assignments will be performed in the generated constructor in the given order
    private val g = gcd(numer, denom)
    private val reducedNumer = numer / g
    private val reducedDenom = denom / g
 
    println("I'm inside the constructor!")
 
    // auxiliary constructor
    def this(integer: Int) = this(numer = integer, denom = 1)
 
    // note use of "override" keyword
    override def toString: String = numer + "/" + denom
 
    // when a method is just a mutator; note lack of "="
    def print { // return type is Unit (like Java's void)
        println(this)
    }
    // silly "if-else" expression example
    def isNonZero: Boolean = true if numer != 0 else false
}
 
object Rational {
    // constants use UpperCamelCase
    val OneHalf = new Rational(1, 2) // "new" still needed for instantiations
}
```

##Design-by-Contract
```scala
def addNaturals(nats: List[Int]): Int = {
    require(nats forall (_ >= 0), "List contains negative numbers") // can throw IllegalArgumentException
    nats.foldLeft(0)(_ + _)
} ensuring(_ >= 0, "Result is not a natural")
```

### Abstract related types
```scala
class Beverage
abstract class Drinker {
    type DrinkOfChoice <: Beverage
    def drink(d: DrinkOfChoice)
}
 
class Alcohol extends Beverage
class Alcoholic {
    type DrinkOfChoice = Alcohol
    override def drink(d: Alcohol) {...}
}
 
class Soda extends Beverage
class Child {
    type DrinkOfChoice = Soda
    override def drink(d: Soda) {...}
}
// Scala ensures that a Child never drinks Alcohol, only Soda
```

### Further Reading
* [Twitter's "Scala School" pages](http://twitter.github.io/scala_school/)
* [Twitter's "Effective Scala" document](http://twitter.github.io/effectivescala/)
* Scala collections library design document
