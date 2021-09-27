---
layout: post
title:  "Manifesto"
---
The main themes of these essays are:

- <u>Notations</u> - dividing work up into small chunks and giving each chunk its own mini-language.
- <u>Software Architecture</u> - It is my feeling that most existing programming languages are geared towards implementation of details instead of description of Software Architecture.  For example, any language that requires the programmer to describe types or to use an operator, such as `+`, is a language of implementation details.  I favour the use of dataless languages for describing Software Architectures.  I use the name DI - Design Intent - when discussing pure Software Architecture devoid of implementation details.
- <u>DaS</u> - Diagrams as Syntax.  There is no good reason why programming languages should not be built using hybrids of diagrams and text.  In fact, most Software Architectures start out life as diagrams on whiteboards.  Parsing and compiling diagrams is at least as easy as parsing and compiling text.  I strive to show the basics of doing so.  (FYI - DaS is not "Visual Programming").
- <u>Asynchronous Software Components</u> - Snapping software together like LEGO® blocks[^2].
- <u>Concurrency</u> - Computers are concurrent.  Most people understand concurrency.  Children learn hard realtime notations at an early age, e.g. music lessons.  Programmers have tried to force computing into cubby-holes using only synchronous methods, which has caused a great deal of accidental complexity.
- <u>Removing Dependencies</u> - Programmers cannot "plug" components together if the components contain dependencies on other components.  We see problems manifest themselves with the use of code libraries and APIs.  Tools (like `npm` and `make`) that help manage dependencies only help in overlooking the elephant in the room.
- <u>Simplicity</u> - Formal methods and mathematical notation were supposed to make it "easier" to "reason about programs".  I think that we've hit an asymptote where formal methods are actually making it harder - than necessary - to reason about programs.  Most programmers think that multitasking is a difficult problem, while I feel that it is easy[^1].  I argue that the main reason for this problem of anti-simplicity is the (failed) idea that we need to use only a single programming language and that we must force-fit every problem into that single language.  I favour the use of multiple notations for a given problem.  I think that technologies like PEG[^3], make it possible to invent notations rapidly and to change the way we think about programming.  I argue that we need to discard the notion of GPLs - General Purpose Languages - and focus on *paradigms* and on the *problems-at-hand*.
- <u>Isolation</u> - Isolation between components is more important than formal proofs, statelessness and all of the other buzzwords.  Isolation is not obvious to achieve - for example, calling a function by using its name is anti-isolationist.
- <u>Programs that write programs</u> - I think that we need to invent languages and syntaxes that cater to machine-readability, and, we need to extend compiler-ism into more general problem solving and computing.  Compilers are programs that write programs - their input is HLL syntax and their output is in the form of triples.  Compiler technology can be extended to transpiler technology, e.g. notations (little languages) that transpile to Python/JS/etc.
- <u>Computers are machines</u>.  Machines do the boring, repetitive work, humans do the thinking.
- <u>Computers Are More Than Just Calculators</u>.  Computers are machines that can perform sequences of operations (functions of time) and control other machines, as well as calculating things.

[^1]:I spent most of my working life designing and building embedded computing solutions.
[^2]: The fact that current technologies (libraries, objects, functions, etc.) don't give us snap-ability raises interesting questions. For example, our view of a flat soup of multiple types inhibits snap-ability.
[^3]: PEG is Parsing Expression Grammars.  I like Ohm-JS the best, at present, https://github.com/harc/ohm

## Highlights

If I were to highlight certain articles, I would choose:

- [Software Development Roles](https://guitarvydas.github.io/2020/12/10/Software-Development-Roles.html)
- [Call return spaghetti](https://guitarvydas.github.io/2020/12/09/CALL-RETURN-Spaghetti.html)
- [Failure Driven Design](https://guitarvydas.github.io/2021/04/23/Failure-Driven-Design.html)
- [Asynchronous Thinking](https://guitarvydas.github.io/2021/07/06/Asynchronous-Thinking.html)
- [The ALGOL bottleneck](https://guitarvydas.github.io/2020/12/25/The-ALGOL-Bottleneck.html)

but, then, I already know what I mean.  

YMMV.

# See Also

[Blog](https://guitarvydas.github.io)

[Table of Contents](https://guitarvydas.github.io/2021/09/21/Table-of-Contents-Sept-17-2021.html)

[Videos](https://www.youtube.com/channel/UC2bdO9l84VWGlRdeNy5)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
