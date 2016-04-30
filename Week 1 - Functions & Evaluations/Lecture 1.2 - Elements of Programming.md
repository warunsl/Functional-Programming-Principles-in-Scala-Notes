# Lecture 1.2 - Elements of Programming

- Elements of a programming language:
    + Primitive expressions representing the simplest elements.
    + Ways to combine expressions.
    + Ways to abstract expressions, which introduce a name for an expression by which it can be referred to.

- REPL stands for Read-Eval-Print-Loop
    + Scala's REPL can either be invoked by installing a standard scala distribution and typing `scala` on the console.
    + Or can be invoked by installing SBT, Scala Build Tool and typing `sbt console` on the console.

- Evaluation of an expression
    1. Take the left most operator.
    2. Evaluate it's operands (left before right).
    3. Apply the operator to the operands.
    A name is evaluated by replacing it with the RHS of it's definition.
    The evaluation stops when the process results in a value.

- Defining functions
    + `def square(x: Double) = x * x`
    + `def sumOfSquares(x: Double, y: Double): square(x) + square(y)`
    + Function parameters come with a type: `variable-name: type-name`
    + Return type are optional and can be defined as `def square(x: Double): Double = ...`
    + Primitive types are capitalized. Ex: Boolean, Double, Int

- Evaluation of functions
    + Evaluate the function arguments from left to right.
    + Replace the function application by the functions' right hand side (the body)
    + At the same time, replace the formal parameters of the function by the actual arguments.
    + This scheme of evaluation is called the substitution model.

- Substitution model
    + Reduce the expression to a value.
    + Can be applied to all expressions as long as they do not have side effects.
        * Example of an expression having side effect; `a++`
        * Evaluating this expression results in returning the old value of `a` and at the same time incrementing the value of `a`.
        * Such a side effect can not be evaluated with the substitution model,
    + Termination of evaluation
        * Not all expressions reduce to a value. `def loop: Int = loop`
        * Can be fixed by changing the evaluation strategy.

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