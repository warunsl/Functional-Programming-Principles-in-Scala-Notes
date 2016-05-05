# Lecture 1.4 - Conditionals and Value Definitions

### Conditional Expressions
+ `if-else`
    * It is used for expressions, unlike in Java where it is used for statement.
    * `def abs(x: Int): Int = if (x > 0) x else -x`

### Boolean expressions
+ Constants: `true` or `false`
+ Negation: `!b`
+ Conjunction: `b && c`
+ Disjunction: `b || c`

### Rewrite rules for Booleans
+ `!true` is `false`
+ `!false` is `true`
+ `true && e` is `e`
+ `false && e` is `false`
+ `true || e` is `true`
+ `false || e` is `e`  
    Last four expressions are referred to as short-circuit evaluation.

### Value definitions
+ Values can be defined either with a `def` or a `val`.
+ 'def' is used to define a variable of the form 'by-name'. It's right hand side is evaluated on each use.
+ 'val' is used to define a variable of the form 'by-value'. It's right hand side is evaluated at the point of the definition itself.

        val x = square(2) 'x' is always 4.
        def y = square(2) 'y' is evaluated on each use.
+ `def`, `val` and expression termination

        def loop: Int = loop
        def x = loop // Not evaluated at definition.
        val x = loop // Evaluated at the definition and results in an infinite loop.

### Exercise
+ Write function `and(x, y)` such that `and(x, y) == x && y`

        def and(x: Boolean, y: Boolean): Boolean = {
            if (x) y else false
        }
    This would work fine if the second argument expression evaluates to a value. Will not work for `and(x, loop)`
    So the function signature should be `def and(x: Boolean, y: => Boolean): Boolean`
+ Write function `or(x, y)` such that `pr(x, y) == x || y`
+ 
        def or(x: Boolean, y: Boolean): Boolean = {
            if (x) true else y
        }
