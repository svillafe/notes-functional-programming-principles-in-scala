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













