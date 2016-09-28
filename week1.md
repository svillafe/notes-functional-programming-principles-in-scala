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

`scala> def square(x : Double) = x * x`

The functions parameter comes with their type which is given after a colon:

`def power(x: Double, y:Int): Double = ...`

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

Scala normally uses **call-by-value**. I practice CBV is more performance than CBN, because it avoids this repeated re-computation of argumentsthat is done by CBN. In addition, CBV behaves better and is more predictable in a mix context of imperative and functional programming like Scala. Nevertheless, if the type of a function parameter starts *=>*, it uses call-by-name.




 
