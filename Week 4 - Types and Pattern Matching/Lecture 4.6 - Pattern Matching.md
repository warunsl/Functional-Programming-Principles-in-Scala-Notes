# Lecture 4.6 - Pattern Matching

### Case Classes
- A case class definition is similar to a normal class definition except that it is preceded by the modifier `case`. Example:

        trait Expr
        case class Number(n: Int) extends Expr
        case class Sum(e1: Expr, e2: Expr) extends Expr
    
    - For a case class, the Scala compiler implicitly defines companion objects with apply methods
        
            object Number {
                def apply(n: Int) = new Number(n)
            }
            object Sum {
                def apply(e1: Expr, e2: Expr) = new Sum(e1, e2)
            }
    
    This lets us use constructs like `case Number(n)` and `case Sum(e1, e2)` in pattern matching as below.
    
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

- Exercise

        object Test {
          trait Expr
          case class Number(n: Int) extends Expr
          case class Sum(e1: Expr, e2: Expr) extends Expr
          case class Prod(e1: Expr, e2: Expr) extends Expr
          case class Var(name: String) extends Expr

          def nestOperations(e1: Expr, e2: Expr): String = {
            val l = e1 match {
              case Number(n) => n.toString
              case Prod(x, y) => show(x) + " * " + show(y)
              case Var(s) => s
              case Sum(x, y) => "(" + show(x) + " + " + show(y) + ")"
            }
            val r = e2 match {
              case Number(n) => n.toString
              case Prod(x, y) => show(x) + " * " + show(y)
              case Var(s) => s
              case Sum(x, y) => "(" + show(x) + " + " + show(y) + ")"
            }
            l + " * " + r
          }

          def show(e: Expr): String = e match {
            case Number(n) => n.toString
            case Sum(e1, e2) => show(e1) + " + " + show(e2)`
            case Prod(e1, e2) => nestOperations(e1, e2)
            case Var(s) => s
          }
          show(Sum(Number(1), Number(2)))
          show(Sum(Prod(Number(2), Var("x")), Var("y")))
          show(Prod(Sum(Number(2), Var("x")), Var("y")))
        }
