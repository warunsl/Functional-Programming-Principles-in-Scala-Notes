# Lecture 5.3 - Implicit Parameters

- The merge function from the previous lecture worked only for `Int`s. Making it generic to all types is not as simple as it seems. We could do:

      def merge[T](xs: List[T], ys: List[T]): List[T}

  But we use a comparison operator in the body of the function (`<`) that is not defined for arbitrary types `T`

- There are a couple of ways to fix this:
    * Pass the comparison function as an additional parameter to `merge`. Like this:

          def merge[T](xs: List[T], ys: List[T])(comp: (T, T) => Boolean): List[T}

      then in the body of the function where we do a comparison, we can do `if (comp(x, y))` instead of `if (x < y)`.

      The function call to `merge` in this case would be:

          merge(List(1, 3, 5), List(2, 4, 6))((x: Int, y: Int) => x < y)
          merge(List("apple", "oranges"), List("bananas", "pineapple"))((x: String, y: String) => x.compareTo(y) <= 0)

      In the above function definition and calls, it is good to have the comparison function as the last parameter. That gives the compiler flexibility to look at the types of the parameters in the first argument to `merge` and implicitly decide on the parameter types of the comparison function. So we could actually define it as:

          merge(List(1, 3, 5), List(2, 4, 6))((x, y) => x < y)
          merge(List("apple", "oranges"), List("bananas", "pineapple"))((x, y) => x.compareTo(y) <= 0)

    * We could parameterize the `merge` function with `scala.math.Ordering[T]`:

          def merge(xs: List[T], ys: List[T])(ord: Ordering[T])

      then in the body of the function where we do a comparison, we can do `if (ord.lt(xs, ys))`

      The function call to `merge` would be `merge(List(1, 3, 5), List(2, 4, 6))(Ordering.Int)`

      A further improvement to this would be to mark the ordering function parameter to `merge` as `implicit`:

          def merge(xs: List[T], ys: List[T])(implicit ord: Ordering[T])

      The benefit of doing this is that we no longer need to pass an additional parameter from the `merge` function call. We can just do:

          merge(List(1, 3, 5), List(2, 4, 6))

      and the compiler will deduce the appropriate `Ordering` type by looking at the parameter types in the call to `merge`

