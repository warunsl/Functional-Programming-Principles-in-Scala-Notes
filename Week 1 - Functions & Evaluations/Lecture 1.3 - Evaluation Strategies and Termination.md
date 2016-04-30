# Lecture 1.3 - Evaluation Strategies and Termination

- Evaluation strategies
    + Call by value
        * Interpreter reduces the function arguments to values before rewriting the function application.
        * Every function argument is evaluated exactly once.
    + Call by name
        * Interpreter applies function to unreduced arguments.
        * A function argument is not evaluated if it is unused in the function definition (evaluation of the function body).
    + Both strategies reduce to the same final value if:
        * The reduced expression consists of pure functions.
        * Both evaluations terminate.
        * If CBV of an expression evaluation terminates, its CBN evaluation terminates too. Other direction is not true.
            Example:

                def loop: Int = loop
                def first(x: Int, y: Int) = x
                first(1, loop)

            Under Call by value, it tries to reduce the second parameter `loop` and gets into an infinite loop.
            Under Call by name, the second parameter is not reduced at all since it is not used in the function definition.
    + Scala uses CBV. CBV does not involve repeated computation of the function arguments.
        * For expressions in general, Call by Value is exponentially faster in computation compared to CBN.
        * Avoids repeated computation of argument expressions.
        * Scala lets you force computation of an expression by using CBN. `=>` is used to achieve that.

                def firstImproved(x: Int, y: => Int) = x

        Here `y` is passed by name and not value. And infinite loop is avoided.