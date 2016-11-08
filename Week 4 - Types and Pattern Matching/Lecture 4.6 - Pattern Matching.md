# Lecture 4.6 - Pattern Matching

### Case Classes
- A case class definition is similar to a normal class definition except that it is preceded by the modifier `case`. Example:

        trait Expr
        case class Number(n: Int) extends Expr
        case class Sum(e1: Expr, e2: Expr) extends Expr
        
- Pattern Matching is a generalization of `switch` constructs from other languages such as Java, C. It is expressed in Scala using the keyword `match`.

- Example:
    
        def eval(e: Expr): Int = e match {
            case Number(n) => n 
            case Expr(e1, e2) => eval(e1) + eval(e2)
        }
        
- A `MatchError` exception is thrown if no pattern matches the value of the selector.

- Pattern Matching constraints:
    * Can be constructed from constructors(as in the example above), variables, wildcard patterns, constants.
    * The same variable name can occur only once in a pattern. Ex: `sum(x, x)` is not a valid pattern.
    * Names of constants should begin with a capital letter with exception of nil, true and false.
    
### Decomposition with Pattern Matching
- In the decomposition example from the previous lecture, `eval` was defined as a function as opposed to a method of the trait. With Pattern Matching, `eval` can be defined as a method of the trait `Expr`
 
        trait Expr {
            def eval: Int = this match {
                case Number(n) => n
                case Sum(e1,e2) => e1.eval + e2.eval
            }
        }