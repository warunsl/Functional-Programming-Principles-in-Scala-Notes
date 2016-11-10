# Lecture 5.1 - More Functions on Lists

### Sublists and element access on lists
- `xs.length`
- `xs.last`
- `xs.init` - All list containing all elements of `xs` except the last one.
- `xs take n` - A list consisting of first `n` elements of `xs` or `xs` if `xs` has elements fewer than `n`.
- `xs drop n` - Rest of the elements of `xs` as a list after `take`ing `n` elements.
- `xs(n)` - Or `xs apply n`. The element of `xs` at index `n`.

### Creating new lists
- `xs ++ ys` - List containing all elements of `xs` followed by all elements of `ys`
- `xs.reverse`
- `xs updated (n, x)` - List containing all elements as `xs` except with `x` at the index `n`

### Finding elements
- `xs indexOf n` - Index of the first element matching `n`, `-1` otherwise.
- `xs contains n` - `xs indexOf n >= 0`

### Implementation of last
        
        def last[T](xs: List[T]): T = xs match {
            case List() => throw new Error("last of an empty list.")
            case List(x) => x
            case y :: ys => last(ys)
        }

### Implementation of init

        def init[T](xs: List[T]): List[T] = xs match {
            case List() => throw new Error("init of an empty list.")
            case List(x) => List()
            case y :: ys => y :: init(ys)
        }

### Implementation of concat

        def concat[T](xs: List[T], ys: List[T]): List[T] = xs match {
            case List() => ys
            case z :: zs => concat(zs, ys)
        }
        
### Implementation of reverse

        def reverse[T](xs: List[T]): List[T] = xs match {
            case List() => xs
            case y :: ys => reverse(ys) ++ List(y)
        }
        
### Exercise
- Implement `removeAt(x, xs)` which removes the element at index `x` from the list `xs`

        def removeAt[T](x: T, xs: List[T]): List[T] = xs take x ::: xs drop x + 1

- Flatten a list of lists to a list
