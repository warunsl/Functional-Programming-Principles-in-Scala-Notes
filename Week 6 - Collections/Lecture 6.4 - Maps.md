# Lecture 6.4 - Maps

- Maps are special in Scala since they are both iterables and functions.
- A map of type `Map[Key, Value]` is a data structure that associates keys of type `Key` with values of type `Value`
- Declaring:
    
        val romanNumerals = Map("I" -> 1, "V" -> 5, "X" -> 10)

- Maps are also functions, meaning they can be used anywhere a function can. For example we can do `romanNumerals("V")`
- If an element does not exist in a map we get a `NoSuchElementException`.
- To check if a map contains a key we can use the `get` method.

        romanNumerals get "M"
        
    This returns `Option[java.lang.String] = None`

### Option Type
- An `Option` type is defined as:

        trait Option[+A]
        case class Some[+A](value: A) extends Option[A]
        object None extends Option[Nothing]
        
- The expression `map get key` returns
    * `None` if the `map` does not contain the `key`
    * `Some(x)` if `map` associates the `key` with value `x`

- Since `Option`s are defined as case classes, they can be decomposed with pattern matching

        def getValue(romanNumeral: String): Int = romanNumerals.get(romanNumeral) match {
            case Some(value) => value
            case None => "Missing data"
        }

### Sorted and GroupBy
- `sortWith` takes a comparator function. `sorted` sorts based on the natural ordering of the datatype of the collection.
- Example:

        val fruits = List("apple", "pear", "orange", "pineapple")
        fruits sortWith (_.length < _.length) // gives List("pear", "apple", "orange", "pineapple")
        fruits.sorted // gives List("apple", "orange", "pear", "pineapple")

- `groupBy` partitions a collection into map of collections based on a function `f`
    
        fruit groupBy (_.head) // gives scala.collection.immutable.Map[Char,List[String]] = Map(p -> List(pear, pineapple), a -> List(apple), o -> List(orange))

- Exercise: Create a class for polynomials and implement the `+` function

        class Poly(val terms: Map[Int, Double]) {
            def + (other: Poly): Poly = new Poly(terms ++ (other.terms map adjust))
            def adjust(term: (Int, Double)): (Int, Double) = {
                val (exp, coeff) = term
                terms get exp match {
                    case Some(c1) => exp -> (coeff + c1)
                    case None => exp -> coeff
                }
            }
        }

- Maps are partial functions. Applying a map to a key that does not exist in the map would lead to an exception.

- The operation `withDefaultValue` makes maps behave more like complete functions.

        val romNumerals = romanNumerals withDefaultValue "Unknown"
        
- With default values the addition of polynomials can be simplified as:

        class Poly(terms0: Map[Int, Double]) {
            val terms = terms0 withDefaultValue 0.0
            def + (other: Poly): Poly = new Poly(terms ++ (other.terms map adjust))
            def adjust(term: (Int, Double)): (Int, Double) = {
                val (exp, coeff) = term
                exp -> (coeff + terms(exp))
            }
        }
