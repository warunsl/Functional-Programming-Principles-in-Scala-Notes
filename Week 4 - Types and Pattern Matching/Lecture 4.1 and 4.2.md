# Lecture 4.1 - Functions as Objects

### Functions as objects
- Scala's numeric types and `Boolean` type can be implemented as normal classes.
- Functions types are treated as classes and function values as objects.
- Every function type A => B is an abbreviation for the class `scala.Function1[A, B]` which is defined roughly as:

        package scala
        trait Function1[A, B] {
           def apply(x: A): B
        }

   - Functions in scala are objects with `apply` methods.
   - The number of parameters a function can take is currently set to 22.
- An anonymous function such as `(x: Int) => x * x` is expanded to:

        { 
          class AnonFunc extends Function1[Int, Int] {
            def apply(x: Int) = x * x
          }
          new AnonFunc
        }

      or with a shorter anonymous class syntax

        new Function1[Int, Int] {
          def apply(x: Int) = x * x
        }

### Expansion of function calls
- A function call like `f(a, b)` is expanded to `f.apply(a, b)`
- A function value 

        val f = (x: Int) => x * x
        f(7)

   would be translated to

        val f = new Function1[Int, Int] {
          def apply(x: Int) = x * x
        }
        f.apply(7)

- Methods are not objects. If it were, then it's class would have a `apply` method which would in turn be expanded to a class definition. It would be an infinite definition and substitution.
- If a method name is used in a place where a function type is expected, it is converted automatically to a function value.

### Exercise
- For the `IntList` class previously defined, define 3 functions in it such that users can create lists of length 0, 2 by doing `IntList()`, `IntList(1)` and `IntList(1, 2)`

        trait List[T] {
          def isEmpty: Boolean
          def head: T 
          def tail: List[T]
        }

        class ConsCell(val T: Int, val tail: List[T]) extends List[T] {
          def isEmpty: Boolean = false
        }

        class NilCell extends List[T] {
          def isEmpty: Boolean = true
          def head: Nothing = throw new NoSuchElementException("Nil head")
          def tail: Nothing = throw new NoSuchElementException("Nil tail")
        }

        object List {
          def apply[T](): List[T] = new NilCell
          def apply[T](a: T): List[T] = new ConsCell(a, new NilCell)
          def apply(a: T, b: T): List[T] = new ConsCell(a, new ConsCell(b, new NilCell))
        }

- Good to know - [Peano numbers](https://wiki.haskell.org/Peano_numbers#Peano_number_types)