---
layout: post
title:  "Nesting and Scoping"
---

It seems that just about every problem in programming is solved by applying nesting (aka scoping).

Think: Nested Russian Dolls.

Nesting leads to isolation.

Nesting is the same as _containment_.

[_A motivating example, can be found in the "Scanner" section, below._]

# Restricted Pathways
Properly-nested components communicate only along well-defined pathways.

Pathways cannot cross the boundaries of a container, except via well-defined _ports_.

Spaghetti-anything implies that the principles of nesting have been broken. 

Thinking about - and specifying - nesting leads to development of languages, DSLs, mini-DSLs (SCNs), APIs, etc.

"Opcodes" hide the details of silicon from us and allow us to use ICs and CPUs.

"Structured Programming" prescribed a method to de-spaghetti-fy the use of GOTOs[^goto].

[^goto]: GOTOs are not a problem. Unrestricted use of GOTOs is a problem. The structured use of GOTOs was a breakthrough idea. GOTOs are needed in Denotational Semantics (GOTOs have been re-branded as CPS).

"Local Variables" prescribed a way to use variables that didn't get one into trouble as a project scaled upwards. We learned how to stop using global variables and how to nest variables (scoping).[^globals]

[^globals]: In fact, global variables are not the problem - unrestricted (unnested) use of global variables is the problem. Scoping gives us locality-of-reference. We can reason about program more easily if we can "see" all of the variables in one eye-full.

OOP taught us how to nest data even further. [_Aside: before OOP, came modules._]

Likewise, State is not a problem, but, unnested (unrestricted) use of state is a problem. Assign-once and FP try to attack the problem by eliminating state, instead of isolating it (nesting it).

Time is considered to be a problem akin to the problem of global variables.

# Diagrams

Nesting is containment.

Diagrams can show containment conveniently.

# Time

Time is considered to be a problem akin to global variables.

"This happens before that" does not mean the same as "that happens before this".

Mathematics and FP conquer the problem of time by eliminating it. 

History is time. 

Time is integral to reality. 

Eliminating time from a notation is but a band-aid.

Q: How can we nest time?

A: An interesting starting point would be Harel StateCharts.

A: We might differentiate between the uses of state. OOP deals with case-on-type. StateCharts and state machines deal with history. 

We often schmoo both kinds of things into the same paradigm, when using GPLs. We use variables to encode history AND we use variables to encode type. 

We have used unrestricted variables to encode history. This practice has given State a bad name.

OOP showed us how to encapsulate data. 

Harel StateCharts showed us how to encapsulate state (and control-flow[^cf])

[^cf]: Control-Flow is not the same as data.  OO style encapsulation does not work well for control-flow.

# Scanner - Motivating Example
This is a simplified example...

What does the following expression mean?
```
x-y
```

In most GPLs, this means "subtract y from x", but, in some PLs (e.g. Lisp and Rebol) this means "the variable x-y". In these languages, "-" is just another character and has no further meaning, "x-y" is similar in meaning to "xay" or "x_y".

In languages that allow "-" to be used as a normal character, we need to write
```
x - y
```
to mean "subtract y from x".  I.E. we need to surround the "-" with breaking-spaces.

How can you parse this?

The meaning of "x-y" is context-dependent (a fancy way of saying "it depends on the parsing history").

What does "-" mean? We don't know until we see the context that it is used in.

If we see "x" followed by "-" followed by "y", it means the variable called "x-y".

If, on the other hand, we see "x" followed by a space followed by "-" followed by a space followed by "y, it means (the variable) "x" then (the function) "-" then (the variable) "y".

Actually, there is no problem in parsing the above, if you use state machines.

If you disallow the use of state machines, recognizing the above becomes harder (not impossible, just harder).

Indecision:
- Computers and internet and blockchain and p2p, etc, etc, are all time-based constructs.
- Theory has shown us that we can express many ideas, succinctly, without the use of state machines.

So, should we disallow the use of state machines, or should we allow the use of state machines?

The answer is: both.

This all comes back to nesting and layering.

If you try to define _just one_ language to do _everything_, you will run into trouble when you try to do certain things[^seq].

[^seq]: E.G. building a music sequencer instead of a calculator.

What is needed is a way to use layers and to define the restrictions at each layer - e.g. this layer uses no state machines, this other layer uses state machines, etc, etc.

# Language Layering - Language Nesting

We need PLs that nest inside each other like Russian nesting Dolls.

We have already had a taste of this kind of thing, using UNIX shells as one language and PLs (say Python, JS, etc.) as another language.

In my opinion, UNIX shells "went too far" and tried to give us abilities that were already available in other PLs (like variables, string concatenation, etc.).

UNIX shell language gives us
1. pipes
2. isolation
3. a bunch of other stuff (featuritis).

Q: How do we create nested languages?

A: We have already seen this in programs like the C preprocessor, languages with pragmas, etc.

## Multiple Syntaxes

What we want is a syntax for state machines and another syntax for data definition, and, we want these syntaxes to be orthogonal, and, we want to lay them over each other like cartoon acetates and layers in PhotoShop.

## Source-to-Source Transpilation

We already kindof use multiple syntaxes for programming. 

We write code in PL syntax, and use compilers to transpile the syntax from PL syntax into assembler syntax.

We want syntax-to-syntax transpilers.

We want syntax-to-syntax transpilers that are easy-to-write, easy-to-read, easy-to-use, etc., etc.

# Nesting Recipe

The recipe for nesting is:

Ensure strict lines of communication where a Child component can only send messages to its Parent component (the Parent decides whether to route the message upwards to its parent, or, downwards to another child). 

## Nesting in Business

Nesting is kinda like departments in business, where it is frowned-upon to go over your boss' head.

# Scalability

Nesting is a necessity for scalability.

You can't scale something if it depends on something else.

Corollary: You can only scale something by dragging in all of the things that it depends on.

Symptom: If your scaling chunk-size is big, then the chunk contains too many dependencies.

Memory: you can't share memory across isolated chunks.

CPU: you can't share CPUs across isolated chunks (CPU sharing is called "time sharing").

Internet: composed of many chunks, where each chunk is a complete computer (with its own CPU(s), with its own memory, etc, etc).

PL: Does your PL (programming language) allow you to express the code for scalable chunks, or, does it only allow you to express the code inside-of a chunk? Thread libraries are just that: libraries. PLs that have threading glue-ons are no better than thread libraries.[^threads]  

What about SQL? SQL is a DSL for data construction and querying. I think that SQL suffers from the same problem that threads do. SQL is not neatly integrated, layered, into most PLs.  SQL also suffers from featuritis - opening a distributed database is different from simply querying a database. What happens if you can't open a database due to networking issues? That kind of issue should be relegated to a distributed-control-flow language.

[^threads]: Threads (and threading libraries, and derivatives) are kludges meant as band-aids to allow us to continue using the synchronous paradigm for programming asynchronous components.

CALL/RETURN: CALL/RETURN implies synchronous operation. Synchronous operation implies dependency. Hence, CALL/RETURN impedes scalability.[^callreturn]

[^callreturn]: Note that FP and Relational Programming are backing into ways for removing CALL/RETURN. HTML can be considered in this light, too (ignoring JS).

# See Also

[Asynchronous Thinking](https://guitarvydas.github.io/2021/07/06/Asynchronous-Thinking.html)
[Blog](https://guitarvydas.github.io)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
