# Lecture 4.7 - Lists

- Lists are immutable. Arrays are mutable.

- Lists and Arrays are homogeneous i.e., elements of a list must be all of the same type.

- Defining lists
    
        val fruits = List("apples", "oranges", "pears")
        val nums = List(1, 2, 3, 4)
        val empty = List()
        val ll = List(List(1, 2, 3), List(4, 5, 6))
        
  Note: We don't use `new` to create a new list.

- Lists are recursive, Arrays are flat.

- Lists are constructed from an empty list `Nil` and the construction operation `::`. The above list examples are actually defined as:

        val fruits = "apples" :: ("oranges" :: ("pears" :: Nil))

- Operators ending with `:` associate to the right. So the cons operator `::` is a method of the right operand. The expression
        
        val nums = 1 :: 2 :: 3 :: Nil
        
  is equivalent to
  
        Nil.::(3).::(2).::(1)
        
- The three fundamental operations on Lists are `isEmpty`, `head` and `tail`.

- Lists and pattern matching are used often. Insertion sort as an example. 

        def isort(xs: List[T): List[T] = xs match {
            case Nil => Nil
            case y :: ys => insert(y, isort(ys))
        }
        
        def insert(x: T, xs: List[T]): List[T] = xs match {
            case Nil => List[T](x)
            case y :: ys => if (x < ys.head) x :: xs else y :: insert(x, ys)
        }