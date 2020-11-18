## What is functional programming? 

We construct our programs using only pure functions
in other words, functions have no side effects.

Example of side effects:
  - Modifying a variable
  - Modifying a data structure in place
  - Setting a field on an object
  - Throwing an exception or halting with an error
  - Pringint to the console or reading the user input
  - Reading or writing to a file

### Function has no side effects

RT - *referential transparency* 
What this all means is that in any program, the
expression can be replaced by its result without changing the
meaning of the program. And we say that a *function is pure*
if calling it with RT arguments is also RT.  


Example 1:

```scala
val x = "Hello"
val r1 = x.reverse
val r2 = x.reverse 

// If we would replace all occurances of the term x with the expression referenced by x, as follows
val r1 = "Hello".reverse
val r2 = "Hello".reverse 
```
This transformation doesn’t affect the outcome. The values of r1 and r2 are the same as before, 
so x was referentially transparent. What’s more, r1 and r2 are referentially transparent as well,
so if they appeared in some other part of a larger program, they could in turn be replaced with their values throughout and it would have no effect on the program.


Example 2:
```scala
val x = new StringBuilder("Hello")
val r1 = x.append(", World").toString
// r2: java.lang.String = Hello, World, World 

val r2 = x.append(", World").toString
// r2: java.lang.String = Hello, World, World

```





