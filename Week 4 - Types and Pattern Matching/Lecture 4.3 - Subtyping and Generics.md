# Lecture 4.3 - Subtyping and Generics

### Polymorphism
- The two types of polymorphism are:
   - Subtyping - Allows us to pass instances of a subtype where a base type was required.
   - Generics - Allows us to parameterize types with other types.
  
- Interactions between Subtypes and Generics:
   - Bounds
   - Variance - defines how parameterized types behave under sub-typing. It defines inheritance relationships of parameterized types, such as whether `Set[String]` is a subtype of `Set[AnyRef]`

- In Scala, generics by default have nonvariant subtyping. So, sets with different element types would never be in a subtype relationship. i.e., `Set[String]` will not be a subtype of `Set[AnyRef]`

- Covariance can however be explicitly specified as

        trait Set[+T] { ... }
   
  Prefixing the type with `+` indicates that the subtyping is covariant for that parameter.
  
- Contravariance can be specified as

        trait Set[-T] { ... }
  
  if `T` is a subtype of `S` this would imply that `Set[S]` is a subtype of `Set[T]`

- Assume we have a generic trait `Queue` and `enqueue` is a method in it. Let us define a subclass of queues that specializes the element type to `Int` and overrides the `enqueue` method as:
 
         class StrangeIntQueue extends Queue[Int] {
            override def enqueue(x: Int) = {
                println(math.sqrt(x))
                super.enqueue(x)
            }
         }
    
We can now define a sequence of operations which results in an error as follows
 
    val x: Queue[Any] = new StrangeIntQueue
    x.enqueue("abc")
    
We can avoid this error by using bounds (lower bounds in this case) by defining the `enqueue` method as:

    class Queue[+T] {
        def enqueue[U >: T](x: U) {...}
    }
    
`U >: T` defines `T` as the lower bound for `U` . As a result, U is required to be a supertype of T.
If `U <: T`, then `T` is the upper bound for `U`. It is also possible to mix a lower bound with an upper bound as so: `[T >: S <: U]`

### Further reading
- Type Parameterization, Chapter 19, Programming in Scala
- [Liskov Substitution Principle](https://en.wikipedia.org/wiki/Liskov_substitution_principle)