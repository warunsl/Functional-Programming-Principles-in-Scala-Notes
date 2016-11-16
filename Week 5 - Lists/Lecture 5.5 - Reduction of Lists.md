# Lecture 5.5 - Reduction of Lists

- A common operation on lists is to combine the elements of a list using a given operator. For example:

        sum(List(x1, ..., xn)) = 0 + x1 + x2 + ... + xn
        product(List(x1, ..., xn)) = 1 * x1 * x2 * ... * xn

  A simple way to define this function would be:

        def sum[T](xs: List[T]): T = xs match {
            case Nil => 0
            case y :: ys => y + sum(ys)
        }

- This pattern can be abstracted out using a generic method called `reduceLeft`

        def sum(xs: List[Int]) = (0 :: xs) reduceLeft ((x, y) => x + y)
        def product(xs: List[Int]) = (1 :: xs) reduceLeft ((x, y) => x * y)

- A simpler way to write the function `((x, y) => x * y)` would be `(_ * _)`.
    Every `_` represents a new parameter going from left to right.

        def sum(xs: List[Int]) = (0 :: xs) reduceLeft (_ + _)
        def product(xs: List[Int]) = (1 :: xs) reduceLeft (_ * _)

- A more general form of `reduceLeft` is `foldLeft`. `foldLeft` is like `reduceLeft` but takes an accumulator `z` as an additional parameter. Also, `foldLeft` works with empty lists unlike `reduceLeft`

        def sum(xs: List[Int]) = (xs foldLeft 0)(_ + _)
        def product(xs: List[Int]) = (xs foldLeft 1)(_ * _)

    * Application of `foldLeft` and `reduceLeft` unfold on trees that lean to the left.
    * They have two dual functions `foldRight` and `reduceRight` which produce trees that lean to the right.
    * For operators that are associative and commutative, `foldLeft` and `foldRight` are equivalent.
    * Sometimes only one of the two operations are appropriate.
    * Example: Consider the task of concatenating two lists.

            def concat[T](xs: List[T], ys: List[T]): List[T] =
                (xs foldRight ys)(_ :: _)

        In this example if we had used `foldLeft` instead of `foldRight` the types would not have matched and it would be a syntax error.

- Exercise:
    * Define `length` in terms of `foldRight`

            def lengthFun[T](xs: List[T]): Int = (xs foldRight 0)((x, y) => 1 + y)

    * Define `map` in terms of `foldRight`

            def mapFun[T, U](xs: List[T], f: T => U): List[U] = (xs foldRight List[U]())((x, y) => f(x) :: y)