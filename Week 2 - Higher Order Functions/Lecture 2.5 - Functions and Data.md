# Lecture 2.5 - Functions and Data

### Classes
+ Typical class definition:

        class Rational(x: Int, y: Int) {
          def numer = x
          def denom = y
        }

    * The above definition introduced two member variables, and defined a constructor for them.
    * Since `numer` and `denom` are `def`s above, they are called by name and hence computed every time they are called (when the object is instantiated)
    * We could as well make them 'val's
    * `toString` is the method that is called when we try to print an object. Override this to control the way objects of the class are printed.

+ Functions that are defined in the class are called methods.

+ Exercise:
    * Add a method `neg` that negates the rational.
    * Add a method `sub` to subtract two rational numbers.

          class Rational(a: Int, b: Int) {
            def numer = a
            def denom = b
            override def toString(): String = numer + "/" + denom
            def add(that: Rational): Rational = {
              new Rational(numer * that.denom + denom * that.numer, denom * that.denom)
            }

            def neg(): Rational = new Rational(-numer, denom)
            def sub(that: Rational): Rational = this.add(that.neg())
          }

          val aRational = new Rational(1, 2)
          val bRational = new Rational(1, 4)
          val cRational = new Rational(1, 8)

          println(aRational.sub(bRational).sub(cRational))
