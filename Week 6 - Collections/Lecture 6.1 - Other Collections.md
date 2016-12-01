# Lecture 6.1 - Other Collections

### Other Sequences
- `List`s are linear. Access to the first element is faster compared to the middle element of the list or the last element.

- Scala library has another collection that has a more balanced access pattern: `Vector`
    * It is structured as a tree internally.
    * For upto 32 elements it is structured as an `Array`
    * If there are more than 32 elements in the `Vector`, the 32 elements at the root level become pointers to 32 child `Array`s.
    * If those run out another level is added and so on.
    * Number of accesses for an element in the `Vector` is equal to the depth of the vector tree.
 
- If the use case requires using the head or tail of a list and recursing then `List` is a better data structure. If however we have bulk operations like `map`, `fold` or `filter` then, `Vector` is a better data structure.

- `Vector`s are created analogously to lists:

        val nums = Vector(1, 2, 3)
        val names = Vector("Bob", "James")

    * `Vector`s support all of the same operations of `List`s except `::`. Instead of `x :: xs` there are:
        + `x :+ xs` which adds the element `x` to the end of `xs`
        + `x +: xs` which adds the element `x` to the beginning of `xs`
        + In both the notations above, `:` points to the sequence.
    
    * The way the elements are addded to an immutable vector is to
        + Copy the leaf node of the vector containing 32 elements.
        + Assuming there is space to add another element, the new element is added to this new leaf node.
        + Then a copy is created of the parent of the leaf node with the last pointer to this new leaf node and all other pointers intact.
        + This process is repeated all the way to the root of the `Vector` internal tree.
        + The complexity of adding an element to `Vector` is therefore proportional to the height of the tree i.e., log (N) to the base 32. N being the total number of elements in the `Vector`
    
### Collection hierarchy
- The base class of `List` and `Vector` is `Seq`, the class of all sequences.
- `Seq` itself is a sub class of `Iterable`

                    Iterator
                    /   |   \
                 Seq   Set  Map
               /  |  \\
              /   |   \ IndexedSeq
             /    |   /\  |
          List  Vector  Range  
          
    * `Seq`, `Set` and `Map` are sub-classes of `Iterator`.
    * `List`, `Vector`, `Range` and `IndexedSeq` are sub-classes of `Seq`
    * `Vector` and `Range` are sub-classes of `IndexedSeq`

- `Array`s and `String`s support the same operations as `Seq` and can be converted to sequences when needed.
- Another `Seq` is `Range`. Three operators are defined on `Range`:
    * `to`: `1 to 5` would give `scala.collection.immutable.Range.Inclusive = Range(1, 2, 3, 4, 5)`
    * `until`: `1 until 5` would give `scala.collection.immutable.Range = Range(1, 2, 3, 4)`
    * `by`: `1 to 10 by 3` would give `scala.collection.immutable.Range = Range(1, 4, 7, 10)`

### Sequence operations
- `xs exists p`
- `xs forall p`
- `xs zip ys`
- `xs.unzip`
- `xs.flatMap f`
- `xs.sum`
- `xs.product`
- `xs.max`
- `xs.min`

### Example:
- Scalar product: Sum of the products of the corresponding elements of two vectors.
    
        def scalarProduct(xs: List[Int], ys: List[Int]): Int = (xs zip ys).map(x => x._1 * x._2).sum
        
    We could also use pattern matching to achieve the same thing as:
    
        def scalarProduct(xs: List[Int], ys: List[Int]): Int = (xs zip ys).map{ case (x, y) => x * y }.sum

- Check for primality (a non optimal yet concise approach):

        def isPrime(n: Int): Boolean = (2 until n) forall (d => n % d != 0)
