# Lecture 4.2 - Subtyping and Generics

### Polymorphism
- The two types of polymorphism are:
   - Subtyping - Allows us to pass instances of a subtype where a base type was required.
   - Generics - Allows us to parameterize types with other types.
  
- Interactions between Subtypes and Generics:
   - Bounds
   - Variance - defines how parameterized types behave under sub-typing. It defines inheritance relationships of parameterized types, such as whether `Set[String]` is a subtype of `Set[AnyRef]`
