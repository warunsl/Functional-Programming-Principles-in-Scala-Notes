# Lecture 1.7 - Tail Recursion

### Tail Recursion
+ Example
        def gcd(a: Int, b: Int): Int =
          if (b == 0) a else gcd(b, a % b)

        def factorial(n: Int): Int =
          if (n == 0) 1 else n * factorial(n - 1)

+ If a function calls itself as it's last action, the function's stack frame can be reuse.
+ In general, if the last action of a function consists of calling a function (which may be the current function itself), one stack frame can be used for both functions. Such calls are called tail-calls.
+ The `gcd` function above is tail recursive because the last task of the function is to call itself.
+ The `factorial` function is not tail recursive since the last action of the function is to multiply `n` with the result of the function call.
+ It can be converted to a tail recursive function as follows
        def factorial(n: Int): Int = {
          def factorialTailRec(n: Int, productSoFar: Int): Int = {
            if (n == 1) productSoFar
            else factorialTailRec(n - 1, productSoFar * n)
          }
          factorialTailRec(n, 1)
        }
+ If you expect your function to run into deep levels of recursion converting it into tail recursion is a good idea.
+ In order to force that an implementation is tail recursive, `@tailrec` annotation can be used.
