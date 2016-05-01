# Lecture 2.1 - Higher-Order Functions

- Higher order functions
    + Functions that either take other functions as parameters or return functions as results.
    + Provides a flexible way to compose programs.

            // Sum of all integers between a and b
            def sumInts(a: Int, b: Int): Int = {
              if (a > b) 0 else a + sumInts(a + 1, b)
            }

            // Sum of cubes of all integers between a and b
            def cube(a: Int): Int = a * a * a
            def sumCubes(a: Int, b: Int): Int = {
              if (a > b) 0 else cube(a) + sumCubes(a + 1, b)
            }

            // Sum of factorials of all integers between a and b
            def sumFactorials(a: Int, b: Int): Int = {
              if (a > b) 0 else fact(a) + sumFactorials(a + 1, b)
            }

            These can be generalized as follows:
            `f(n) for all values of n between a and b`

            In Scala, it can be generalized as:

            def sum(f: Int => Int, a: Int, b: Int): Int = {
              if (a > b) 0
              else f(a) + sum(f, a + 1, b)
            }

    + `f: Int => Int` is the way to define a function parameter
    + Generalising `sumInts`, `sumCubes` and `sumFactorials`

            def sumInts(a: Int, b: Int): Int = sum(id, a, b)
            def sumCubes(a: Int, b: Int): Int = sum(cube, a, b)
            def sumFactorials(a: Int, b: Int): Int = sum(fact, a, b)

            where

            def id(a: Int): Int = a
            def cube(a: Int): Int = a * a * a
            def fact(a: Int): Int = if (a == 0) 1 else a * fact(a - 1)

- Function Types
    + `A => B` is a function type. Stands for a function that takes type A and returns type B. Ex: `Int => Int` is the type of function.

- Anonymous functions
    + Passing functions as parameters usually leads to creation of smaller functions. Defining a name for each of these is tedious. Just like `def str = "Hello"; println(str)` is more tedious compared to `println("hello")`
      We could do that because strings exist as literals. Scala allows making functions as literals. These are called anonymous functions.
    + Syntax
      `(x: Int) => x * x * x`
      `(x: Int)` is the parameter of the function and `x * x * x` is it's body.
    + `sumInts`, `sumCubes` and `sumFactorials` using anonymous functions can be defined as:

            def sumInts(a: Int, b: Int): Int = sum(x => x, a, b)
            def sumCubes(a: Int, b: Int): Int = sum(x => x * x * x, a, b)

    + Exercise: Replace the `sum` function as a tail recursive function
      Solution

            def sum(f: Int => Int, a: Int, b: Int, sumSoFar: Int): Int = {
              if (a > b) sumSoFar
              else sum(f, a + 1, b, f(a) + sumSoFar)
            }
