# Lecture 1.6 - Blocks and Lexical Scope
### Blocks in Scala
+ A block is delimited by braces.
+ Blocks are expressions and can be used where other expressions can be used.

### Blocks and visibility
+ Definitions inside a block are only visible inside the block. Definitions made outside the block are visible inside as long as there is no redefinition of the same name within the block.
+ If there are more than one expression/definitions in a line, a semi-colon is needed.
+ If there is a statement which spans multiple lines, parentheses can be used to group them.
