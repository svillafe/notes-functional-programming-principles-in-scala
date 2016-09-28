#Week 1
##1. 1 Programming Paradigms

###Paradigms: 

The paradigms escribes distinct concepts or thoughts patterns in some scientific discipline.

**Main Paradigms:**
	
* Imperative
* Functional
* Logic

**Orthogonal:** Object Oriented Programming

*** 

**Imperative programming is about**:
	
* Modifying mutable variables
* Using assigments
* Using control structures e.g. if-else, loops, breaks, etc

> The most common informal way to understand imperative programs is as insctructions sequence for a Von Neumann computer.

A **Von Neumamm** machine has the following main components:
	
* Processor
* Memory
* Bus (32 / 64 bit) which connects the two previous components.

There is a strong correspondence between:
* mutable variable and memory cells
* variable deferences and load instructions
* control structures and jumps

In the end, pure imperative programming is limited by the Von Neumann bottleneck. One tends to conceptualize data structure word-by-word. 

See paper: [Can Programming Be Liberated from the von Neumann Style? A Functional Style and Its Algebra of Programs](http://www.thocp.net/biographies/papers/backus_turingaward_lecture.pdf) by John Backus

*** 

In order to scale up we need to define high level abstractions: `collections`, `polynomials`, etc.

Ideally we need to develope **Theories**. A theory consist of: 
* One or more datatypes
* Operations on these datatypes
* Laws that describes relationships between values and operations
* *Normally* theory does not describe mutations.

Since the theories do not admit mutation and also mutation can destroy useful laws in the theories, if we want to implement high-level concepts following their mathematical theories, there is no place for mutation. As a result let's:
* concentrate on defining theories for operators
* avoid mutations
* have powerfull ways to abstract and compose functions

***

**Functional programming is about**:

In a **restricted** sense, *functional programming* means programming without mutable variables, asigment, loops, and other imperative control structures. In particular functions can be values that are produced, consumed and composed. This behaviour becomes easier in a *functional programming language*.

A **functional programming language**, is one whici does not have mutable variables, assigments or imperative control structures. In a *functional programming language*, functions are **first class citizens** which mean:
* Functions can be defined anywhere, including inside other functions.
* Functions can be passed as parameters to functions and they can be returned as results.
* As for other values, there exists a set of operators to compose functions.

***

**Functional Programming Languages:**
* Restricted
  * Pure List, XSLT, XPath, XQuery, FP
  * Hasckell (without I/O Monads)
* Using the wide definition:
  * Lisp
  * SML
  * Hackell (Complete language)
  * Scala
  * Smalltalk, Ruby
  
***

Recomended books: 
  * [Structure and Interpretation of Computer Programs](https://www.amazon.co.uk/Structure-Interpretation-Computer-Electrical-Engineering/dp/0262510871)
  * [Programming in Scala](https://www.amazon.co.uk/Programming-Scala-Martin-Odersky/dp/0981531687/ref=sr_1_1?s=books&ie=UTF8&qid=1475074139&sr=1-1&keywords=Programming+in+Scala)
  
***

##1. 2 Elements of Programming

Every **non-trivial language** provides primitive: 
* expressions that represents the simplest elements of the language
* some ways to combine expressions
* ways to abstract expressions. Abstraction means that we introduce a name for an expression and then further on we can reference the expression by its name. 

**REPL (Read-Eval-Print-Loop):**
 * The interactive shell lets one to write expressions and respond with their value.  
 * The Scala REPL can be started by typing `scala` if you have a regular distribution of Scala. In case you installed `sbt`, you can run the command `sbt console`. 
 
*** 

**Evaluation:**
 
A non-primitive expression is evaluated as follows:
 
1. Take the leftmost operator (subject to the rules of presedent)
2. Evaluate its operands (left before right)
3. Apply the operator to the operands
 
A name is evaluated by replacing it with the right hand side of its definition.
The evaluation process stops once it results in a value.

E.g.: 

(2 * pi) * radius
*(First we look for the pi number)*

(2 * 3.14159) * radius
*(Second we perform the arithmetic operation on the left)*

(6.28318) * radius
*(Third the variable is replaced)*

(6.28318) * 10
*(Finally we perform the final arithmetic operation)*
62.8318

***

**Definitions:**

Definitions can have parameters:

```scala
scala> def square(x : Double) = x * x
```

The functions parameter comes with their type which is given after a colon:

```scala
def power(x: Double, y:Int): Double = ...
```

If a return type is given it follows the parameter list.

**Evaluation of Function Applications:**

1. Evaluate all function arguments, from left to right
2. Replace the function application by the function's right hand side, and, at the same time 
3. Replace the formal parameters of the function by the actual arguments

This scheme of expression evaluation is called the **substitution model**. 

The idea underlying this model is that all evaluation does is **reduce an expression to a value**. 

It can be applied to all expressions, **as long as they have no side effects**.

The substitution model is formalized in the lambda calculus, which gives the foundation for functional programming.

**Ways of evaluation:**

There are two ways of evaluating the same expression: *call-by-value* and *call-by-name*. **call-by-value** has the advantage that it evaluates every function argument only once. On the other hand, **call-by-name** has the advantage that a function argument is not evaluated is the corresponding parameter is unused in the evaluation of the function body.

Both strategies reduce to the final value as long as: 

* the reduce expression consists of pure functions
* both evaluations terminate



##1. 3 Evaluation Strategies and Termination

Both **call-by-name** (CBN) and **call-by-value** (CBV) reduce to the same value as long as both evaluations terminate. Let's analyze the case where termination is not guaranteed.

There is a theorem that says:
> If CBV of an expression *e* terminates, then (=>) the CBN evaluation of *e* terminates too. The other direction is not true.

**Scala's evaluation strategy:**

Scala normally uses **call-by-value**. In practice CBV is more performance than CBN, because it avoids this repeated re-computation of argumentsthat is done by CBN. In addition, CBV behaves better and is more predictable in a mix context of imperative and functional programming like Scala. Nevertheless, if the type of a function parameter starts *=>*, it uses call-by-name.

##1. 4 Conditionals and Value Definitions

**Conditionals Expressiona**

Scala has a conditional expression `if-else`

The Scala's `if-else` looks like the Java's one, but is **used for expressions not statements**.

For example:

```scala
   def abs(x:Int) = if (x >= 0) x else -x
```
In the example above we can see that the `if-else` is an expression, it is not an statement where you have to set a variable and then return a variable. The `x>=0` is a expression of type `Boolean` and that expression is sometime called predicate.

**Boolean Expressions**

```scala
true false //Constants
!n         //Negation
a && b     //Conjuction
a || b     //Disjunction
a <= b, a < b, etc //comparison operations
```

In general if a expression is legal in Java, you can expect that is going to be legal in Scala as well.

In the evaluation process, note that `&&` and `||` do not always need their right operand to be evaluated.

**Value definitions**

The function parameters can be passed **by value** or **by name** and the same distinction applies to *definition*. 

The **def** form is called **by-name** because *its right hand side is evaluated on each use*. 

There is also a **val** form which is **by-value**. In other words, *the right-hand side of a val definition is evaluated at the point of the definition itself*.

For example:

```scala
val x = 2
val y = square(x)
```
In the example, **y** refers to 4, not to the expression *square(2)*.

The different between **def** and **val** becomes apparent when the right hand does not terminate. 

Given:

```scala
def loop: Boolean = loop
```

A definition like:
```scala
def x = loop
```
will terminate becauhse we are given only a new name to loop, but
```scala
val x = loop
```
will lead to an infinite loop, becuase it evaluate and execute a infinite loop.



##1.5 Implementation in Scala

One pecularity of Scala is that the return type of a recursive function is needed to be always given. The reason for that is that in order to compute the return type, the Scala compiler will have to look at the right-hand side and because the function is recursive, it stacked in a cycle.
To break the cycle, we require that recursive functions must always has explicit return types. 

##1.6 Blocks and Lexical Scoping

**Nested functions:**
It is good style to split up a task into many small functions. Nevetheless all this sub functions only matter for the implementation of the task. **_We would not like users to access these functions directly._**. 

One way to achieve this, is to put all the auxiliarly functions inside the main task definition. For example:

```scala
def task(x : Double) = {
	def aux1(x : Double) = ???
	def aux2 = ???

	aux1(x)
}
```

This is also known as **Blocks**. A block has the following properties: 
* It is delimited by braces { ... } 
* It contains a sequence of definitions or expressions.
* The last element of a block is an expression that **defines its value**.
* This return expression can be preceded by auxiliary definitions.
* Blocks **are expressions**, a block may appear everywhere an expression can be used.

**Blocks and visibility:**
There are two main rules regarding visibility and blocks: 

1- The definitions inside a block are only visible from within the block.

2- The definitions inside a block _shadow_ definitions of the same names outside the block.

**Semicolons:**

In Scala the semicolons at the end of the line **are in most cases optional**. On the other hand, **if there are more than one statements on a line**, they need to be separated by semicolons. 

The problem arise when expression are too long to fix on one line. There are two ways of overcome this problem:

* You could write the multi-line expression in parentheses, because semicolons are never inserted inside (...)

* You could write the operator on the first line, becuase it tells to the Scala compiler that the expression is not yet finished.











 
