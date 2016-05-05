# Lecture 2.6 - More Fun With Rationals

### Classes (contd)
+ `private` members in classes

  class Rational(a: Int, b: Int) {
    private def gcd(a: Int, b: Int): Int = if (b == 0) a else gcd(b, a % b)
    private val g = gcd(a, b)
    def numer = a / g
    def denom = b / g
    ...
  }

+ In the above class definition if methods `numer` and `denom` are called a lot, it makes sense to compute their values once by defining them as `val` than `def`.

+ We can add restrictions to the fields of the class using `require` as below:

        class Rational(x: Int, y: Int) {
          require(y > 0, "Denominator must be a positive value.")
          def numer = x
          def denom = y
        }

    * If the restriction in the 'require' fails, it raises an `IllegalArgumentException`. `require` is used to enforce a precondition.
    * `assert` is another way to impose restrictions. It throws an `AssertionError`. `assert` is used to check the code of the function itself.

+ A class implicitly introduces a constructor. It's called the primary constructor. We can add any statement in the body of the class definition and it will execute it during creating an object.

+ Other constructors can be defined with `def this()`

        class Rational(x: Int, y: Int) {
          def numer = x
          def denom = y
          def this(x: Int) = this(x, 1)
          ...
        }
