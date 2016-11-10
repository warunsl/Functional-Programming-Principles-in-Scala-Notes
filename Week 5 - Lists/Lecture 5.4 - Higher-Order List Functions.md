# Lecture 5.4 - Higher-Order List Functions

- Some of the recurring patterns in computations on lists involves:
    * Transforming each element of the list in a certain way.
    * Retrieving a list of all elements satisfying a certain criteria.
    * Combining the elements of a list using an operator.

    Higher order functions makes this easier.

- Applying a function to elements of a list.
    Consider the example of multiplying every element of a list by a factor. It can be written as:

         def multiplyByFactor(xs: List[Int], fc: Int): List[Int] = xs match {
           case Nil => xs
           case y :: ys => y * fc :: multiplyByFactor(ys, fc)
         }

    There exists a higher order function `map` that achieves the same result

        def multiplyByFactor(xs: List[Int], fc: Int): List[Int] = xs map (x => x * fc)

    One way to define `map` would be:

        abstract class List[T] { ...
            def map(f: T => U): List[U] = this match {
                case Nil => this
                case x :: xs => f(x) :: xs.map(f)
            }
        }


- Filtering
    Consider the example of getting all positive numbers from a list. It can be written as:

        def getPos(xs: List[Int]): List[Int] = xs match {
            case Nil => Nil
            case y :: ys => if (y > 0) y :: getPos(ys) else getPos(ys)
        }

    There exists a higher order function `filter` that achieves the same result

        def getPos(xs: List[Int]): List[Int] = xs filter (x => x > 0)

    Variants of `filter`:
    * `filterNot` - Elements of the list not matching the filter criteria
    * `partition` - This is `filter` and `filterNot` in one go. Returns a pair of two lists.
    * `takeWhile` - Returns all elements of the list till the index for which the function holds true.
        Example: For a list `List(2, -4, 5, 7, 1)`, `takeWhile(x => x > 0)` returns `List(2)`
    * `dropWhile` - Returns all elements of the list after the index for which the function holds true.
        `dropWhile` for above would be `List(-4, 5, 7, 1)`
    * `span` - Combines results of `takeWHile` and `dropWhile` as a pair and returns it.

- Exercise
    Define a function `pack` that packs consecutive duplicates of list elements into sublists.
    Example: `pack(List("a", "a", "a", "b", "c", "c", "a"))` should return `List(List("a", "a", "a"), List("b"), List("c", "c"), List("a"))`

        def pack[T](xs: List[T]): List[List[T]] = xs match {
            case Nil => Nil
            case y :: ys =>
                val (first, rest) = xs span (z => z == y)
                first :: pack(rest)
        }

    Using `pack` define `encode` that returns `List(List("a", 3), List("b", 1), List("c", 2), List("a", 1))` for the same input.

        def encode[T](xs: List[T]): List[(T, Int)] = pack(xs) map (x => (x.head, x.length))