# Lecture 2.2 - Currying

### Functions that return other functions
+ We can define the `sum` function in another way too. In a way that returns a function.

        def sum(f: Int => Int): (Int, Int) => Int = {
          def sumF(a: Int, b: Int): Int = {
            if (a > b) 0
            else f(a) + sum(a + 1, b)
          }
          sumF
        }

    * `sum` is now a function that takes a function as an argument and returns another function as result.
    * The return type after the `:` in `def sum(f: Int => Int): (Int, Int) => Int = {` denotes that `sum` is returning a function that takes two `Int` arguments and returns an `Int`
    * We can then define `sumInts`, `sumCubes` and `sumFactorials` as

            def sumInts = sum(x => x)
            def sumCubes = sum(x => x * x * x)
            def sumFactorials = sum(fact)

    * We can get rid of `sumInts`, `sumCubes` and `sumFactorials` altogether and have

            sum(cube)(1, 10)
            sum(fact)(1, 5)

    * Function application associates left to right `sum(cube)(1, 10) === (sum(cube))(1, 10)`

+ Functions that return other functions are used frequently in Scala and Scala provides a easier syntax to achieve that.

        def outer-func(outer-func-params): <signature-of-returned-func> = {
          def inner-func(inner-func-params): <inner-func-return-type> = {
            <inner-func-body>
          }
          inner-func
        }

  can be replaced by `def outer-func(outer-func-params)(inner-func-params): <outer-func-return-type> = {}`

        def sum(f: Int => Int)(a: Int, b: Int): Int = {
          if (a > b) 0
          else f(a) + sum(f)(a + 1, b)
        }

+ Exercise
    * Write a product function that calculates the product of the values of a function for points on a given interval

              def product(f: Int => Int): (Int, Int) => Int = {
                def productF(a: Int, b: Int): Int = {
                  if (a > b) 1
                  else f(a) * productF(a + 1, b)
                }
                productF
              }

    * Write factorial in terms of product

              def factInTermsOfProduct(a: Int): Int = product(x => x)(1, a)

    * Can you write a more general function, which generalizes both `sum` and `product`

              def generalizeSumAndProduct(f: Int => Int): (Int, Int, Int) => Int = {
                def subFunction(unitValue: Int, a: Int, b: Int): Int = {
                  if (a > b) unitValue
                  else {
                    if (unitValue == 0)
                      f(a) + subFunction(unitValue, a + 1, b)
                    else
                      f(a) * subFunction(unitValue, a + 1, b)
                  }
                }
                subFunction
              }

        Better solution:

              def MapReduce(f: Int => Int, combine: (Int, Int) => Int, zero: Int)(a: Int, b: Int): Int = {
                if (a > b) zero
                else combine(f(a), MapReduce(f, combine, zero)(a + 1, b))
              }

              def product(f: Int => Int): (Int, Int) => Int = MapReduce(f, (x, y) => x * y, 1)
              def sum(f: Int => Int): (Int, Int) => Int = MapReduce(f, (x, y) => x + y, 0)
