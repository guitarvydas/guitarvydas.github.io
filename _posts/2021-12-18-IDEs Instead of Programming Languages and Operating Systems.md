---
layout: post
title:  "IDEs Instead of Programming Languages and Operating Systems"
---

# The Goal
The goal of programming is to control a computer.
## Secondary Goals
### Secondary Goal: Describe Architecture to Other People
It is desirable to describe designs to other people.

For example, in the construction industry, 
- Architects use drawings and 3D models to describe designs to Engineers
- Engineers use blueprints to describe design details to Construction Workers (Implementors).

Both of these kinds of communication - drawings, models - are used to describe aspects of the design to other people.

#### Tertiary Goal: Automated Checking of Descriptions

In the Construction Industry, drawings are checked manually.

Using computers, it becomes possible to write software that checks aspects of design documentation.

Programmers and programming language designers strive to write software that checks design documents (usually in the form of textual "code").  

IMO, language designers miss the fact that automated checking is only a tertiary goal.

### Secondary Goal: Production Engineering

Once a design has been vetted (by Architects, Engineers, Testers, etc.), the design can be optimized along a number of dimensions - this is called Production Engineering.

Typically, Production Engineering in software tends towards making a low-cost version of the software, usually taking into account hardware costs that the software is to run on.

Most popular so-called General Purpose programming Languages are actually DSLs for Production Engineering.  I include Haskell, Python, JavaScript, etc., etc., in this list of popular GPLs.

In fact, any programming language that provides the `+` operator, or, `arrays` and `lists`, or, `user-defined types`, is usually designed as a DSL for Production Engineering.

`Compilation` is geared towards Production Engineering.  All languages can be interpreted, but, only some languages can be compiled, after making various trade-offs in the languages themselves.  Interpretation helps with Design and Vetting, Compilation helps with Production Engineering. [Note that, neither is actually geared towards only DI[^3] - communicating designs to other people.]

[^3]: DI means Design Intent

# Programming Languages Are IDE Wannabes
Programming languages (GPLs[^1]) are only the tip of the iceberg for controlling computers.

[^1]: GPL means General Purpose programming Language.
# Operating Systems Are IDE Wannabes
Operating systems are the only tip of the iceberg for controlling computers.

# IDE Evolution
What do we want in an IDE?

Given that the primary purpose of programming is controlling computers, we want *anything* that helps us program computers.

We *don't* want to use only one-thing in a one-size-fits-all manner.

We see this kind of desire leaking into GPL designs.

For example, REGEXs[^2] have leaked into some GPLs, giving those GPLs two (2) syntaxes.

[^2]: REGEX means REGular EXpression.  A technology lifted from compiler design and made popular in languages like PERL, JavaScript, etc., etc.

As an example of the evolution of IDEs, consider technologies that we already know: C++ and REGEXs.

We want an IDE that has multiple windows that can produce an executable module at the push of a button.

Using only the above already-known technologies, we might expect:
- a window for writing REGEXs, in REGEX DSL syntax,
- a window for writing replacements after REGEX matching has been successful, in REGEX replacement DSL syntax
- a window for writing Production Engineering code in C++ syntax, with some sort of bauble to show where the REGEX pattern matchers pattern replacers are to be inserted.

To illustrate the point, imagine that we want to write a REGEX that replaces all "A"s with "AB"s
- we might write /(A)/ in window 1
- we might write /\\1B/ in window 2
- we might write some C++ in window 3.

In fact, we would probably drop the "/" characters in windows 1 and 2.

In the above example, parentheses are use to "remember" parts of the match, e.g. `(A)` remembers "A" (if matched) and gives it the name `\1`[^6].

[^6]: Standard REGEX syntax is obtuse and, IMO, write-only.  I would suggest replacements to this syntax, but, I believe that REGEX will be superceded by PEG (Ohm-JS), and, it is not worth expending time on improving the syntax.

A simple example of a REGEX visualizer is [regex101](https://regex101.com).

We want something like the REGEX visualizer to become our windows 1 and 2 in our progamming IDE.

Of course, one could re-imagine the above using languages, like Python and JavaScript, that have REGEXs built into them.

## Further Ideas:

I believe that Ohm-JS is better than REGEX.

If we look at the [Ohm-JS IDE](https://ohmlang.github.io/editor/), we see the beginnings of what we want in one of the windows of our futuristic IDE.

We would want to augment the IDE with an Ohm-JS replacement window (a replacment rules for every grammar rule in Ohm-JS.  See the [glue tool](https://guitarvydas.github.io/2021/04/11/Glue-Tool.html) for POC-level ideas for a replacement DSL for Ohm-JS programs.

See [DaS Workbench] for POC-level ideas on multi-window, heads-up displays for pattern matching and replacement.   

See [Transpilation](https://guitarvydas.github.io/2021/07/12/Transpilation.html) for POC-level ideas on how to transmogrify PEG into two separate parts.



# Appendix - See Also
[Blog](https://guitarvydas.github.io)
[Table of Contents as of Dec. 01, 2021](https://guitarvydas.github.io/2021/12/01/Table-of-Contents-December-01-2021.html)
[Videos](https://www.youtube.com/channel/UC2bdO9l84VWGlRdeNy5)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 

