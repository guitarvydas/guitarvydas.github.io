---
layout: post
title:  "Restricting Interfaces (portability, ocg, gcc, λ)"
---
# Restricting Interfaces
The big win in software repeatedly seems to be in restricting interfaces.

Assembler is a restricted API of what is possible using microcode.

APIs are restricted interfaces to applications.

Structured Programming is a way to restrict control flow.

OO (Object Oriented) is a way to restrict data structuring.

Global variables were tamed by scoping (restricting the interface to variables).

λ Calculus is a way to restrict interfaces to
1. functions
2. bound variables

(λ Calculus uses The Stack to create a dynamic chain of containers at runtime. Functions (and closures) are containers with very restricted interfaces (one group of data in, one group of data out (aka parameters and return value(s), resp.))).

## Portability, Retargeting
Research on compilers in the mid-1970s resulted in things like:

- OCG - Orthogonal Code Generator (Cordy), which defined a small set of operations to divide-and-conquer the task of compilation
	- 1. the compiler produces code for generic operations (like "a = b + c")
		- all data is allocated in a uniform manner ([data descriptors](https://dl.acm.org/doi/10.1145/24039.24051]))
		- normalization makes automation easier
		- *condition descriptors* were invented and look a lot like λ of 2 parameters (true and false branches, De Morgan's Laws could be used to manipulate *condition descriptors*)
	- 2. tree-walker produces real code for specific CPUs from the generic code

- RTL - Register Transfer Logic -  (Fraser Davidson Peephole optimizer)
	- used in GCC
	- defines a small set of operations
		- all data is assumed to be allocated in "registers" (fake, virtual)
		- all operations act on "registers"
		- peephole optimizer walks RTL code and produces real code for specific CPUs
		- I built such a peephole optimizer using just AWK (for my 8080 C compiler)

Now, we are dealing with lambda calculus, which defines a small set of operations
	- apply
	- abstraction
	- access bound slot
and, encodes all programs as a combination of these operations.

## Normalization
To reiterate, normalization makes automation easier.

Assembler is easy to compile, because it is normalized to triples
`MOV R0, R1`.

OCG, RTL, [Peter Lee's take on Denotational Semantics](https://www.amazon.ca/Realistic-Compiler-Generation-Peter-Lee/dp/0262121417) all use the same trick - *normalization* (restricting the interface).

*Normalization* makes *divide-and-conquer* easier.

[BTW, parameterization is the anti-thesis of normalization.  Parameterization makes interfaces more complicated (nuanced) instead of making them simpler (less nuanced).  (Aside: we don't need to throw nuance away, just push it to a different view/level).]

[BTW, one of the beauties of Lisp is that its syntax is normalized.  Everything *looks* like a function and everything has a value (i.e. everything is an expression).  This kind of extreme normalization led to the invention of Lisp macros (which happen to look like functions).  λ calculus applied to programming is regurgitating these concepts - everything is a function, every function always returns a value (another function), every function takes exactly one parameter, the type of every parameter is the same (an apply-able function))]
- ## See Also

[Table of Contents](https://guitarvydas.github.io/2021/12/10/Table-of-Contents-Dec-01-2021.html)
[Blog](https://guitarvydas.github.io)
[Videos](https://www.youtube.com/channel/UC9EJr0nKHwadbHUtc5zHdmQ/videos)
[References](https://guitarvydas.github.io/2021/01/14/References.html)
[Books](https://leanpub.com/u/paul-tarvydas.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 