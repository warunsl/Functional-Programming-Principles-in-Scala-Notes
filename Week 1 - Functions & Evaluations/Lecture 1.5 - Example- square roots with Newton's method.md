# Lecture 1.5 - Example: square roots with Newton's method

- Exercises
    + Write function `and(x, y)` such that `and(x, y) == x && y`

        def and(x: Boolean, y: Boolean): Boolean = {
            if (x) y else false
        }

        This would work fine if the second argument expression evaluates to a value. Will not work for `and(x, loop)`
        So the function signature should be `def and(x: Boolean, y: => Boolean): Boolean`

    + Write function `or(x, y)` such that `pr(x, y) == x || y`

        def or(x: Boolean, y: Boolean): Boolean = {
            if (x) true else y
        }

    + Compute `sqrt(x)` using Newton's method:

		  def abs(x: Double) = if (x > 0) x else -x

		  def sqrt(x: Double): Double = {
			def sqrtIter(guess: Double): Double = {
			  def isGoodEnough(guess: Double): Boolean = abs(guess * guess - x) < 0.001
			  def improvedGuess(guess: Double): Double = (guess + x / guess) / 2

			  if (isGoodEnough(guess)) guess
			  else sqrtIter(improvedGuess(guess))
			}
			sqrtIter(1.0)
		  }
		  
		  sqrt(2)

    + Notes:
        * Recursive functions in Scala must have a return type.
        * Functions that are necessary for another function can be nested within the main function to avoid namespace pollution.