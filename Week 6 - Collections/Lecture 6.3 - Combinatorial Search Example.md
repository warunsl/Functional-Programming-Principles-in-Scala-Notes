# Lecture 6.3 - Combinatorial Search Example

### Sets
- `Set`s are a sub-class of `Iterable`s.
- They are defined analogously to a sequence: `val s = Set('b', 'a', 'c')`
- Most operations on Sequences are also available on sets:

        s map (_ + 2)
        s filter (_ startsWith == 'a')
        s.nonEmpty
        `toSet` is an operator that converts a sequence to a set. Ex: (1 to 6).toSet
- Differences between `Set`s and `Sequence`s are:
    * `Set`s are unordered.
    * `Set`s do not have duplicate elements.
    * Fundamental operation on `Set`s is `contains`.

- N queens problem example.
