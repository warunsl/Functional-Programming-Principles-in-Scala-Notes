# Lecture 4.5 - Decomposition

- Suppose we have a hierarchy of classes and want to build a tree-like data structures from the instances of these classes. One way of modeling the data would be to have a trait and a bunch of sub classes extending this trait. The number of method definitions needed in this case will be too high since we would have to override the methods of the traits in each of the sub classes.

- One solution for avoiding this would be to use type tests and type casts i.e., with `isInstanceOf` and `asInstanceOf`. This is discouraged in Scala.

- Suppose we are to define an interpreter for arithmetic operations. Let's assume that the arithmetic operations just include numbers and sum operation.

        trait Expr {
            def isNum: Boolean
            def isSum: Boolean
            def numValue: Int
            def leftOp: Expr
            def rightOp: Expr
        }
        
        class Number(n: Int) extends Expr {...}
        class Sum(leftOp: Expr, rightOp: Expr) extends Expr {...}
        
        def eval(e1: Expr): Int = {...}
        
    Using `isInstanceOf` and `asInstanceOf`, `eval` can be defined as:
    
        def eval(e: Expr): Int =
            if (e.isInstanceOf[Number])
                e.asInstanceOf[Number].numValue
            else if (e.isInstanceOf[Sum])
                eval(e.isInstanceOf[Sum].leftOp) +
                eval(e.isInstanceOf[Sum].rightOp)
            else throw new Error("Error")
            
- If all we are interested in doing is defining a `eval` function for evaluating the expression then, we can define `eval` as a method in the base trait as :

        trait Expr {
            ...
            def eval: Int
            ...
        }
        
    and have the implementations of it in the subclasses as
    
        class Number(n: Int) extends Expr {
            override def eval: Int = n
        }
        
        class Sum(e1: Expr, e2: Expr) extends Expr {
            override def eval: Int = e1.eval + e2.eval
        }
    The short coming with this method is we need to touch all classes (possibly across multiple source files) to add a new method to the trait.

- Another solution involves Scala's Pattern Matching.
