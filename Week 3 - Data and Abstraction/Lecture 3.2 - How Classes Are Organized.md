# Lecture 3.2 - How Classes Are Organized

- Packages
    + Classes and Objects are organised in packages.

            package progfun.examples
            object Hello {}

        This fully qualified object can be used while compiling or running like `scala progfun.examples.Hello`

    + In order to import a named type from a package we do:

            import progfun.examples.Hello
            import progfun.examples.{Hello, Rational}   // imports more than one
            import progfun.examples._                   // imports everything under examples

    + All members of the packages `scala`, `java.lang` and the singleton object `scala.Predef` are auto imported.

- Traits
    + In Scala, a class can have only one superclass.
    + If a class wants to inherit code from more than one supertype we use `traits`.
    + `traits` are declared like an `abstract class` with the keyword  `trait` instead of `abstract class`
    + Classes, objects and traits can inherit from at most one class but from many traits.
    + Classes inherit code from a trait with the `with` keyword.

            class Square extends Shape with Planar with Movable

    + traits cannot have `val` parameters. But unlike interfaces in Java it can contain concrete methods and fields.

- Scala class hierarchy
	+ [Class hierarchy](http://www.scala-lang.org/old/sites/default/files/images/classhierarchy.png)
    + `Scala.Any` is at the top of scala class hierarchy and is the base type of all scala types. It is also the base type that defines universal methods like `toString`, `equals`, `hashCode`, `==`, `!=`, etc
    + `Scala.AnyVal` is a subclass of `Scala.Any` and is the base class of all primitive types like `Byte`, `Int`, `Double`, etc
    + `Scala.AnyRef` is a base type of all reference types. Alias of `java.lang.Object`

- Nothing type
    + `Scala.Nothing` is at the bottom of Scala's type hierarchy. It is a subtype of every other type. There is no value of type `Nothing`
    + Used to signal abnormal termination. If sometimes a function throws an exception or terminates unexpectedly, it's return type is of type `Nothing`.
    + Used as an element type of empty collections.
    + An expression `throw exp` returns type `Nothing`

- Null type
    + `Scala.Null` is the subtype of every reference type.
    + Every reference class type also has `null` as a value.
    + The type of `null` is `Null`
    + `Null` is a subtype of every class that inherits from `java.lang.Object`.
    + It is incompatible with subtypes of `AnyVal`

            val x = null
            val y: String = null
            val z: Int = null       // type mismatch


