# Lecture 6.2 - Combinatorial Search and For-Expressions

- Higher order functions and collections often replace loops in imperative languages.
- Example: Given a positive integer `n`, find all pairs of positive intefers `i` and `j` with `1 <= j < i < n` such that `i + j` is prime.
    * This would involve generate all the pairs of values of `i` and `j` and then check for each pair if `i + j` is prime.
    
            object pairs {
                val n = 7
                (1 until n) map (i =>
                    (1 until i) map (j => i + j))
            }

    * This gives a vector of vectors i.ie., `(IndexedSeq[(Int, Int)])`
    * The reason we got a vector of vectors is because when we used `Range` to generate pairs, Scala can not represent pairs as `Range`, so it represents it as a sub class of `Seq` called `IndexedSeq`. The canonical representation of `IndexedSeq` is a `Vector`
    * However we need to concatenate all element vectors into a single list of pairs. This can be done in one of the two ways:
    
            (1 until n).map(i => (1 until i).map(j => (i, j))).flatten
            (1 until n).flatMap(i => (1 until i).map(j => (i, j)))
    
    Both of these are the same because `xs flatMap f = (xs map f).flatten`
    * Solution for the exercise:
    
            object pairs {
                def isPrime(n: Int): Boolean = (2 until n).forall(n % _ != 0)
                (1 until n).flatMap(i => (1 until i).map(j => (i, j))).filter(pair => isPrime(pair._1 + pair._2))
            }
    
    * The above single line code is very difficult to understand. This can be simplified with for-expressions.
    
### For-Expressions
- A for-expression is of the form:

        for ( s ) yield e
        
    * `s` is a sequence of generators and filters.
    * `e` is an expression whose value is returned by an iteration.
    * A generator is of the form `p <- c` where `p` is a pattern and `c` is an expression whose value is a collection.
    * A filter is of the form `if f` where `f` is a boolean expression.
    * The sequence must start with a generator.
    * OF there are several generators in the sequence, the last generator vary faster than the first.
    * Instead of `( s )`, `{ s }` can also be used and then the sequence of generators and filters can be written on multiple lines without using semicolons.
    
- The exercise can now be written as:

        object pairs {
            def isPrime(n: Int): Boolean = (2 until n).forall(n % _ != 0)
            for {
                i <- 1 until n
                j <- 1 until i
                if isPrime(i + j)
            } yield (i, j)
        }

- Exercise: Rewite the scalar product function using for expressions.

        def scalarProduct(xs: List[Int], ys: List[Int]): Int = (xs zip ys).map(x => x._1 * x._2).sum
