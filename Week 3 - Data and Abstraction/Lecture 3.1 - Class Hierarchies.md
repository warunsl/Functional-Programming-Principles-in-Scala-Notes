# Lecture 3.1 - Class Hierarchies

### Abstract classes
+ Typical abstract class definition:

        abstract class IntSet {
          def incl(x: Int): IntSet
          def contains(x: Int): Boolean
        }

    * `abstract` classes can have method signatures defined in the class without actually having a definition. Removing the `abstract` keyword would cause an error.
    * `abstract` classes cannot be instantiated.

+ Example

        abstract class IntSet {
          def incl(x: Int): IntSet
          def contains(x: Int): Boolean
        }
        class EmptyIntSet extends IntSet {
          def incl(elem: Int): IntSet = new NonEmptyIntSet(elem, new EmptyIntSet, new EmptyIntSet)
          def contains(elem: Int): Boolean = false
          override def toString() = "."
        }
        class NonEmptyIntSet(root: Int, leftSubtree: IntSet, rightSubtree: IntSet) extends IntSet {
          def incl(elem: Int): IntSet = {
            if (elem < root) new NonEmptyIntSet(root, leftSubtree incl elem, rightSubtree)
            else if (elem > root) new NonEmptyIntSet(root, leftSubtree, rightSubtree incl elem)
            else this
          }
          def contains(elem: Int): Boolean = {
            if (elem < root) leftSubtree contains elem
            else if (elem > root) rightSubtree contains elem
            else true
          }
          override def toString() = "{" + leftSubtree + root + rightSubtree + "}"
        }
        val t1 = new NonEmptyIntSet(7, new EmptyIntSet, new EmptyIntSet)
        val t2 = t1 incl 5 incl 9 incl 3 incl 2 incl 1 incl 8 incl 10

  gives

        t1: NonEmptyIntSet = {.7.}
        t2: IntSet = {{{{{.1.}2.}3.}5.}7{{.8.}9{.10.}}}

    * `IntSet` is called the superclass of `EmptyIntSet` and `NonEmptyIntSet`
    * `EmptyIntSet` and `NonEmptyIntSet` are subclasses of `IntSet`
    * Every class extends the base class `Object` even if there is no explicit `extends Object` in the class definition.
    * All direct and indirect superclasses of a class are called its base classes. Ex: `IntSet` and `Object` are base classes of `EmptyIntSet`
    * It is also possible to redefine an existing, non-abstract method definition in a subclass using `override`
    * Code invoked by a method call depends on the runtime type of the object. This is called dynamic binding or dynamic method dispatch.

### Object definitions
+ In the `IntSet` example, there is only a single empty IntSet. It is a overkill to allow users to create multiple instances of it.
+ Such scenarios are better expressed using object definitions.

        object EmptyIntSet extends IntSet {
          def contains(x: Int): Boolean = false
          def incl(x: Int): IntSet = new NonEmptyIntSet(x, EmptyIntSet, EmptyIntSet) // We dropped the 'new'
        }

+ The above snippet defines a singleton object.
+ They are `val`s so `EmptyIntSet` evaluates to itself.

### Programs
+ Each Scala application contains an `object` with a `main` method.
+ After compiling with `scalac`, it can be executed on the command line with `scala <object-name>`
