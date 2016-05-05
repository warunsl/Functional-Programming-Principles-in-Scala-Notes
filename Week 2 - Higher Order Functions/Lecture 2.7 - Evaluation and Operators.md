# Lecture 2.7 - Evaluation and Operators

### Operators
+ Any method with a parameter can be used like an infix operator. Ex: `r.add(s) ==> r add s`
+ Identifiers in scala can be alphanumeric or symbols. Therefore methods like 'add', 'less', 'sub' can be defined as:

        class Rational(x: Int, y: Int) {
          def numer = x
          def denom = y
          def + (that: Rational):Rational = new Rational(numer * that.denom + denom * that.numer, denom * that.denom)
          def neg: Rational = new Rational(-numer, denom)
          def - (that: Rational):Rational = this + that.neg
          def max(that: Rational) = if (this < that) that else this
        }

+ Caveats:
    * If an identifier name ends with a symbol there needs to be space after it. As in `def + (`
    * If we plan to use symbols for an unary operator like in the case of 'neg', we use the keyword `unary`  
      `def unary_- : Rational = new Rational(-numer, denom)`

### Precedence
+ Precedence of an operator is determined by its first character.
+ Order:
    all letters (lowest)  
    `|`  
    `^`  
    `&`  
    `< >`  
    `= !`  
    `:`  
    `+ -`  
    `* / %`    
    special characters(highest)
