# Lecture 3.3 - Polymorphism

### Cons-Lists
+ Concept of cons cell
   * https://en.wikipedia.org/wiki/Cons
   * https://cs.gmu.edu/~sean/lisp/cons/
+ Immutable linked lists are a fundamental data structure in many FP languages. They are made up of:
   * Cons - a cell containing an element and the remainder of the list.
   * Nil - the empty list

### Value paramters
+ Defining a class as

        class Cons(val _head: Int, val _tail: IntList)

   is same as doing

        class Cons(_head: Int, _tail: IntList) {
          val head = _head
          val tail = _tail
        }

### Type paramters
+ In order to define a Cons-List that is generic, we need to generalize the definition. This is done using a type parameter.

        trait List[T]
        class Cons[T](val _head: T, val _tail: List[T]) extends List[T]
        class Nil[T] extends List[T]

+ Type parameters can also be applied to functions.
  Example: Consider a function that creates a single element `List`. It can be defined as:
      def singleton[T](elem: T) = new Cons[T](elem, new Nil[T])
  This function can be invoked for `Int`a as `singleton[Int](1)` or simply as `singleton(1)` and the compiler will deduce the type automatically.
  
+ Type parameters do not affect evaluation in Scala. All type parameters and type arguments are removed before evaluating a program. This is called **type erasure**.

### Polymorphism
+ Usually means that the function types come in many forms.
+ w.r.t programming it means:
   * The function can be applied to arguments of many times. Or
   * The type can have instances of many types.
+ Two forms of polymorphism:
   * subtyping: Instances of subclasses can be passed to a base class.
      Example: In case of `List`, we had `Nil` and `Cons` as subtypes of `List` and wherever a parameter that accepts a `List` as a parameter is encountered, a `Nil` or a `Cons` could be passed.
   * generics: Instances of a function or class are created by type parameterization.
