# Lecture 5.2 - Pairs and Tuples

- List's `splitAt` function returns a pair.

- Pair in Scala is written as `(x, y)`
    
      val pair = ("answer", 42)

- Pairs can be used as patterns:
    
      val (label, value) = pair
        
      scala> val pair = ("answer", 42)
      pair: (String, Int) = (answer,42)
    
      scala> val (label, value) = pair
      label: String = answer
      value: Int = 42
    
- This can be generalized for tuples of more than two elements. A tuple type `(T1, ..., Tn)` is an abbreviation of the parameterized type `scala.Tuplen[T1, ..., Tn]`
    
    As an example, the `Tuple2` class is modeled after the following pattern:
    
      case class Tuple2[T1, T2](_1: T1, _2: T2) {
        override def toString = "(" + _1 + "," + _2 + ")"
      }

- We could have defined `label` and `value` in the above example as

      val label = pair._1
      val value = pair._2
    
    However the pattern matching variant is used since it is shorter over the `_` variant.

- `merge` function of a merge sort algorithm using pattern matching on tuples (pairs)

      def merge(xs: List[Int], ys: List[Int]): List[Int] = {
          (xs, ys) match {
              case (Nil, ys) => ys
              case (xs, Nil) => xs
              case (x :: xs1, y :: ys1) =>
                if (x < y) x :: merge(xs1, ys)
                else y :: merge(xs, ys1)
          }
      }
