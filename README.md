# Functional Programming Principles in Scala

## Course details
Course: https://class.coursera.org/progfun-005  
Instructor: Martin Odersky

## Index
[Week 1: Functions & Evaluations](Week 1 - Functions & Evaluations)  
[Week 2: Higher Order Functions](Week 2 - Higher Order Functions)

## Scala Syntax Summary
- Types can be:
    * Numeric type (`Int`, `Double`, `Byte`, `Short`, `Char`, `Long`, `Float`)
    * Boolean type (`true`, `false`)
    * `String` type
    * Function type (`Int => Int`, `(Int, Int) => Int`)
- Expressions can be:
    * An identifier like `x`, `isGoodEnough`
    * A literal like `0`, `1.0`, `"abc"`
    * A function application like `sqrt(x)`
    * An operator application like `-x`, `y + x`
    * A selection like `math.abs`
    * A conditional expression like `if (x > 0) x else -x`
    * A block like `{ val x = math.abs(y) ; x * 2 }`
    * An anonymous function like `x => x + 1`
- Definitions can be:
    * A function definition like `def sqrt(x: Int): Double = {}`
    * A value definition like `val y = sqrt(2)`
- Parameter can be:
    * Call by value parameter like `(x: Int)`
    * Call by name parameter like `(y: => Double)`

