---
layout: post
title:  "UX - User Experience"
---
## UX - User Experience
It is not *enough* to present all of the options to a user.

The options must be presented in a way that is convenient to the user.

That "convenience" is UX.

## Programming Languages Are IDE Wannabes

Programming languages are IDEs for the act of programming.

Programming languages are stunted IDEs.

Programming languages, currently, are based only on code as text.  

## The Humane Interface

Jef Raskin's "The Humane Interface" is a book that takes a stab at UX design issues. 

## IDEs
### IDEs For Non-Programmers
#### Spreadsheets
#### Word Processors
### Windows
#### Apps and App Stores
### MacOS
### IDEs For Programmers
#### Linux - Original
#### Early, Dynamic Languages
#### REPL
REPLs are aimed at "rapid development", i.e. Design and trying-out Designs.
##### Lisp
##### Forth
##### Etc.
#### Production Engineering
##### Compilers
##### Compiled Languages
Syntax is twisted to appease compilers and allow easier compilability, but UX suffers.

###### Declaration-before-use

Based on mid-1900s biases towards saving memory and CPU time.

The real issue is detection of typos.

Declaration-before-use appeases compilability, but UX suffers (least important stuff comes first).

Legal contracts use declaration-before-use, but are based on
- the fact that contracts are written in text on paper
- our reading style - we read from top to bottom
- machines (computers) don't care - they can access randomly and don't need top-to-bottom arrangement (except to appease compilability).

Simple step forward: declaration *anywhere* (before or after first use).  

JavaScript attempts to achieve this in a clunky way - "lifting" (based on the incremental use of compiler lore, influenced by mid-1900s biases instead of 2000's reality).

The even-more-real issue is "why do we use text?".  Machines (computers) can do more. 

Characters are but non-overlapping grids of fixed-size bitmaps.

We can do more with machines in the 2000's, like using windows.  In fact, my bank statement uses PDF and places *every* character using postscript (a derivative of Forth).  Text-only-based approaches choke on this format, since they "see" single characters instead of strings of characters.  Sigh.

## Theory, Rigor, Completeness, Self-Consistency

Theoretical approaches only solve 1/2 of the problem - the correctness issue.

Theoretical approaches tend not to solve the UX issues - the other 1/2 of the problem.

In fact, UXs in the 2000's suck compared to desktop GUIs of the 1990s.  Emacs has become worse, not better, as far as the UX goes (the screen/buffer flashes randomly).

Draw.io may be rigorous, but the UX sucks.

## Dynamic vs. Static

The rush towards compilability and rigor has ruined the UX-ness of programming languages.

Compiled languages trade off compilability / completeness against UX.

Compilation is an optimization and hurts concurrency (and, hence, parallelization).

The optimization of compilation leads to static binding which leads to twisting of programming languages, trading off PL ease-of-use in lieue of compilability.

## Concurrency

Concurrency-in-the-small doesn't help as much as concurrency-in-the-big-picture.

What we want is to be able to make every operation concurrent and to alleviate the bloated-ness of spawning big processes in lieue of spawning small processes.

Closures and anonymous functions *are* concurrency.

If "systems programmers" didn't hate Lisp and other "dynamic" languages so much, maybe they wouldn't have bothered to build behemoth implementations of closures called Operating Systems with their hands tied behind their backs with assembler and C.

Aside: Anonymous functions - called *lambdas* - preceded the invention of *closures*.  Closures were invented as a way of appeasing compilability concerns.

Closures led to De Bruijn indexing, which is another way of obfuscating the UX.  Forth (nee postscript) obfuscates just fine.

## Lambda Calculus - Bad UX

Quick, what does this program do?
`λ [[0 [λ [0 0] λλλλ [[1 [3 3]] λ [[0 3] 1]]]] $nil]`[^blc]

[^blc]: https://justine.lol/lambda/

The above program is derived through mathematical manipulation.  It is (probably) sound, but its DI[^DI] is not very revealing.

[^DI]: DI means Design Intent.

## Creating UX

Revealing-ness is UX.

Can we wrap the above program in a way that is more humane to the reader?

What is the "science" behind UX design?

We could use Ohm-JS / PEG / etc. to wrap text around this.

But, why stop at text?  Why not use a diagram?  Not necessarily a full-blown VPL, nothing fancy, just a box with some text in it, and some input and output ports.

This used to be called "schematics", and, "drawings", and, "drafting", and, "blueprints".

Instead we continue to use ASCII-art, like `{ ... }`, to represent boxes.  Long after unicode replaced ASCII...

And, now we have SVG, which contains all of the primitives we need to program using diagrams:
1. boxes
2. ellipses
3. text
4. lines.

(Ignore the rest of the SVG stuff 😀 ).

## Code Bloat
IMO, Code Bloat comes from notation-abuse.

If you push a notation "too far", you need to figure out clever ways to abuse the notation to do what you need done.

For example, functional programming is a good notation[^sl] for building fancy, synchronous calculators that obey the 1-in-1-out principle that cannot use mutation.

[^sl]: See Sector Lisp and BLC for an example of how beautifully small this paradigm can be.

Mutation has been grafted onto the functional paradigm, resulting in epicycles like preemption, operating systems, multi-tasking, fairness, semaphores, priority inversion, etc., etc.

Multi-tasking used to be easy.  Loop, test for termination, call code snippet, continue looping.

Instead, we have things like Windows and MacOS and Linux that take the easy-ness out of multi-tasking, so that we can build fancy, synchronous calculators[^calc] that multi-task.

[^calc]: A calculator has exactly one synchronous input and exactly one synchronous output (the input and output can be destructured into several low-level data objects that have different low-level "types", as is already done in compilers).  A calculator cannot have 0 inputs nor 0 outputs.  A calculator cannot have more than 1 input nor more than 1 output.  A calculator cannot sequence things nor track "history".  A calculator cannot respond to asynchronous inputs.  A calculator cannot produce asynchronous outputs.  The callee blocks while waiting for a result from a calculator.  We cannot know if the called calculator will block waiting for results from sub-calculators.  We cannot calculate the throughput of a calculator (at best, we can measure the throughput and cross our fingers hoping that we've measured all edge cases).  Why does all of this matter?  Robotics.  IoT.  Distributed programming (internet, blockchain, etc.).  UX (mouse-clicks).  What about exceptions?  Uh, we had to kludge the functional paradigm to add warts called exceptions.  What about long-running loops and deep recursion?  Infinite loops only happen during development. Loops and recursion are non-starters for distributed language design (if you really, really want a loop, send yourself a feedback message).  What about daemons and servers?  They use the "simple" version of concurrency - loop, create response, continue - there is no need to make them more complicated.  (In fact, there are good reasons - like unintended bugs and security - for de-complicating daemons and servers). 

Programming used to be understandable until we invented textual "programming languages".

Programming used to be about making a machine do what was needed.  

Now, programming is about notation-worship.

We are expected to completely ignore issues like history and sequencing in lieue of building fancier, synchronous calculators.

## Orthogonal Programming Languages

Orthogonal split between
1. data allocation and access
2. operators

Syntax is used for control-flow.

Operands (Data Descriptors, functions, getters, setters) are for data access.

Ohm-JS / PEG / etc. are DSLs for creating parsers.  They make syntax easy-to-design-and-implement.

See OCG (Cordy's Orthogonal Code Generator) for further details.

See Data Descriptors (Holt's Data Descriptor paper) for further details.

## Synonyms
Every name (variable, function, type, etc.) should be associated with a list of synonyms.

Every operator should be associated with a list of synonyms.

The IDE should allow the programmer to turn a dial and get as much detail / as little detail about any syntactic element in a program.

For example, a maintainer might want to see long names for every name/operation when first getting one's feet wet and trying to understand what is going on.

For another example, a theoretician might want to reduce every name down to a single character to be able to "see" the algorithm better.

The programming language should not define what a programmer can see.  The IDE should give the programmer a dial.

I believe that many of our programming languages suffer from schizophrenia, where the language designer has tried to appease the extremes in both camps (above) and has, usually, devised a watered-down version (a union) as the final resulting "general purpose" language.

## See Also
[Names and Data Descriptors](https://guitarvydas.github.io/2022/03/24/Names-and-Data-Descriptors.html)

[Data Descriptors - a compile-time model of data and addressing](https://dl.acm.org/doi/10.1145/24039.24051)
[OCG](https://books.google.ca/books/about/An_Orthogonal_Model_for_Code_Generation.html?id=X0OaMQEACAAJ&redir_esc=y)

[Table of Contents](https://guitarvydas.github.io/2021/12/10/Table-of-Contents-Dec-01-2021.html)
[Blog](https://guitarvydas.github.io)
[Videos](https://www.youtube.com/channel/UC9EJr0nKHwadbHUtc5zHdmQ/videos)
[References](https://guitarvydas.github.io/2021/01/14/References.html)
[Books](https://leanpub.com/u/paul-tarvydas.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" > 
</script> 