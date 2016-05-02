# Lecture 2.3 - Example: Finding Fixed Points

- Fixed point - https://en.wikipedia.org/wiki/Fixed_point_(mathematics)
    + In mathematics, a fixed point (sometimes shortened to fixpoint, also known as an invariant point) of a function is an element of the function's domain that is mapped to itself by the function. That is to say, c is a fixed point of the function f(x) if and only if f(c) = c. This means f(f(...f(c)...)) = fn(c) = c, an important terminating consideration when recursively computing f. A set of fixed points is sometimes called a fixed set. Not all functions have fixed points: for example, if f is a function defined on the real numbers as f(x) = x + 1, then it has no fixed points, since x is never equal to x + 1 for any real number.
    + Function to compute fixed point

            val tolerance = 0.001
            def isCloseEnough(x: Double, y: Double) =
              abs((x - y) / x) / x < tolerance
            def fixedPoint(f: Double => Double)(firstGuess: Double): Double = {
              def iterate(guess: Double): Double = {
                val next = f(guess)
                if (isCloseEnough(guess, next)) next
                iterate(next)
              }
              iterate(firstGuess)
            }

    + Square root function can be expressed in the form of above function as

            def sqrt(x: Double): Double = fixedPoint(y => x / y)(1)

        * In the above function, values of `guess` `iterate` comes up with oscillates between 1 and 2.
        * In order to control the oscillation, we need to make sure successive values do not vary too much.
        * We can average successive values of `next` with an averaging function of the form `f(x) = x + f(x) / 2` i.e.,

                def averageDamp(f: Double => Double)(x: Double): Double = (x + f(x)) / 2

        * Square root function can be improved as follows:

                def sqrt(x: Double): Double = fixedPoint(averageDamp(y => x / y))(1)

    + Above example demonstrates the power of functions returning other functions as results which is central to functional programming.