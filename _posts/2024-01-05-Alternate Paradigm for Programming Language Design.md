# Where Does Sector Lisp's Smallness Come From?

I note that Tunney's Sector Lisp is orders of magnitude smaller than the smallest practical programming language (I believe this to be Lua).

I note that Tunney's Garbage Collector (TGC) is smaller than even McCarthy's original GC (mark-and-sweep), clocking in at about 40 bytes.  TGC is small, TGC is quick, TGC is incremental. 

This smallness comes as a result of slavishly applying the concepts of Functional Programming to the implementation of the language.  

Sector Lisp has no heap, no mutation. None whatsoever. The programmer *cannot* express mutation, assignment or anything that requires a heap.

Sector Lisp is only 436 bytes long with a 40-byte Garbage Collector.  Correlation does not imply causation, but, maybe there's a lesson in here that warrants further study.

# Alternate Paradigm for PL Design

The principle of "no mutation" makes SL essentially useless for what we consider to be programming in the traditional "union of all features" LCD-paradigm of PL design.

Yet, if we accept that SL can't do everything and allow it to stick to expressing parts of programs that are entirely within its sweet spot, we might imagine a possible alternate paradigm for PL design.

Instead of a single union of features, we create a *set* of programming languages and snap them together to form solutions to problems.

In such a paradigm, each altPL would address only a single aspect of PL usage, e.g. 
- stack-based (FP)
	- functional only
	- blocking-call until return
	- fully supporting referential transparency of textual PLs
		- (note that "referential transparency" for DPLs (Diagrammatic Programming Languages) is already well-understood - it's called ICs (Integrated Circuits) and EE)
- LOAD/STORE 
- GOTO
- encapsulation
- Statechart rules for combatting state explosion
- Drakon rules for control flow
- recursion
- looping
- subroutines for saving space 
- subroutines for DRY (Don't Repeat Yourself)
- concurrency
- time-ordering of events
- "pipelines" that are cyclic graphs
- "main loops"
# Syntactic Snapping-Together and Composition
Until fairly recently, it has been considered to be difficult to whip up new programming syntaxes.

The advent of PEG-based technologies - OhmJS is currently my favourite - changes all of that.

It becomes possible to create new syntaxes in minutes.

It becomes possible to switch back to using the technique of "syntax driven translation" as espoused in the implementation of PT Pascal.

It becomes possible to imagine syntaxes geared for human consumption *and* syntaxes geared only for machine consumption.

It becomes possible to build multi-pass applications that have unique syntaxes for each pass, allowing implementors to focus on one issue at a time, e.g. parsing, vs. semantic gathering, vs. semantic checking, vs. assigning data storage allocations, vs. dumb code emission, vs. replacing dumb code with less-dumb code (aka "peepholing"), global optimization, etc., etc.

# Skipping Over Code

One of the features of PEG, and, therefore OhmJS, is the ability to write nano-grammars that "skip over" uninteresting bits of code.  This kind of thing is much more cumbersome to express using CFG and REGEX based technologies.  Because of this cumbersomeness of previous technologies, language designers have tended to avoid this nano-grammar approach.

The apparently-simple addition of matched-pair parsing in PEG allows programmers to write nano-grammars.

In one experiment, I ended up writing something like 15 "passes", each dealing with single - very specific - issues.  Kind of like a chain of macro processors - rewrite phrases that look like "...this...", but, leave the rest alone.

OhmJS enhances the concept of macro processing through its provision of Lexical and Syntactic grammars and the `applySyntactic<...>` operator.

In my experiments, I spawned each pass as a separate process - much like UNIX shell pipelines.  This is not strictly necessary, since it is possible to use OhmJS as a callable subroutine (aka "function") and to call the OhmJS parser/semantic-processor multiple times, each time with a slightly different syntax.

My experimental manifestation of macro processing using OhmJS appears to be "inefficient", dealing with each character one at a time. Yet, the experiments have always run "fast enough" on modern hardware. 

An unforeseen aspect of this approach is that the input languages can be relatively small, which allows a wider range of implementation (in)efficiencies to be employed. Backtracking on modern hardware doesn't hurt as long as the inputs are relatively small. It seems that most anything can be written in one screen-full, which tends to get processed in a blink of the eye.

# Pattern for Skipping Over Code

See 2024-01-05-Macros for Non-Lisp Languages for more information.

Nonsensical nano-grammar:

```
hamburger {
  characters = character+
  character =
    | applySyntactic<Macro> -- macro
    | any -- other
  Macro = "I" "want" "a" "hamburger"
}
```

Input:
```
a b c I want a hamburger d e f

```

Screenshot:
![hamburger grammar](/screenshots/hamburger%20grammar%20Screenshot%202024-01-05%20at%207.25.55 AM.png)
After parsing the input, we output
```
a b c⎨
kitchen.order("hamburger");
⎬d e f
```
where "`⎨...⎬`" delimits a piece of *verbatim* code.  Downstream passes are expected to skip over *verbatim* code, since it has already been preprocessed.

The final output in this simplistic example is:
```
a b c
kitchen.order("hamburger");
d e f
```
In this example, `pass2` inhales the output from the `hamburger` pass and strips off all verbatim brackets.  We *could* mute the other characters by simply outputting nothing. For this example, I didn't bother to do this. In a real example, just about every input phrase will get processed in some way, so muting would be the exception anyway, and less interesting to show.

The working example is in the repo [hamburger](https://github.com/guitarvydas/hamburger)

# Appendix - Language Set Experiments
What is a *set* of languages?  

Basically, I think that syntax is cheap, but, that paradigms are important.

I think that Prolog has a wonderful syntax for expressing *exhaustive search*.  That same syntax is not appropriate for most other things.

I think that Javascript *template strings* and *string interpolation* form a nice syntax for formatting textual output.  Other languages are better than Javascript at just about everything else.

I think that OhmJS has a wonderful syntax for expressing *parsing* based on pattern matching with some backtracking.

I think that */bin/bash* is a good tool for plumbing lumps of code together.

In one experiment, I wrote a tiny DSL (I call it an SCN - Solution Centric Notation) for expressing *semantics* code that is required for building OhmJS applications.  Currently, I call the DSL *RWR* (for ReWRite), but, it's had many different names in the past, like "glue", "fab", "prep", etc.

In another experiment, I bolted Prolog + JavaScript together and used bash to feed the output from one to the other. I built a quickie DSL, based on markdown syntax (yes, markdown can be a programming language syntax, if you continue to insist on using text for programming), for this using OhmJS. I used this combination to build an early version of my DPL technologies *and* augmented the whole thing were very specific checks (more than just type checking) that I call *Design Rules* (name stolen from the same concept in EE). I expressed patterns in a Prolog-y manner and output in a Javascript-y manner.  I used a *bash* pipeline to pipe output from one syntactic phase to the other.  Even though this spawned processes and ran up *swipl* and *node*, the result ran fast enough (seconds) on my relatively new hardware (at that time, an Intel-based MacBook) to allow me to chop up what I was working on into a bunch of small divide-and-conquer pieces and to finish it. 

Note that I didn't even bother to create my own full-blown syntax for the DSL, I just created a transpiler that chopped the input source code up and created `.pl` and `.js` files as necessary, feeding lumps of the input source to each without much more checking - `swipl` and `node` already do a lot of syntax checking and I didn't want to duplicate their efforts.

An example of such DSL source code is https://github.com/guitarvydas/bootstrap2/blob/main/d2fb/das2f/direct_contains.md .

# Appendix - References

### PT Pascal and Syntax-Driven Translation
[PT Pascal and S/SL](https://research.cs.queensu.ca/home/cordy/pub/downloads/ssl/)

### Fraser/Davidson Peepholing - RTL and GCC
Fraser Davidson
[https://www.researchgate.net/publication/220404697_The_Design_and_Application_of_a_Retargetable_Peephole_Optimizer](https://www.researchgate.net/publication/220404697_The_Design_and_Application_of_a_Retargetable_Peephole_Optimizer)

Portable code generator in two passes (Used in gcc)
### Cordy OCG - Orthogonal Code Generation
Cordy

OCG - Orthogonal Code Generator. Portable code generator in two passes, declarative.

[https://books.google.ca/books?id=X0OaMQEACAAJ&dq=bibliogroup:%22University+of+Toronto+Computer+Systems+Research+Institute+Technical+Report+CSRI%22&hl=en&sa=X&ved=2ahUKEwig1Legm8bqAhWvlHIEHYzzBYEQ6AEwBHoECAEQAQs](https://books.google.ca/books?id=X0OaMQEACAAJ&dq=bibliogroup:%22University+of+Toronto+Computer+Systems+Research+Institute+Technical+Report+CSRI%22&hl=en&sa=X&ved=2ahUKEwig1Legm8bqAhWvlHIEHYzzBYEQ6AEwBHoECAEQAQs)

### PEG - Parsing Expression Grammars
Bryan Ford. PEG parsing – the definitive source

[https://bford.info/packrat/](https://bford.info/packrat/)
### OhmJS
Ohm-js
object-oriented language for JS (based on PEG and META-II)
https://ohmjs.org

[https://github.com/harc/ohm](https://github.com/harc/ohm)
### Unfinished Example of Multi-Pass Macro-Processing Chain
https://github.com/guitarvydas/ceptre 
branch bc86474031619d44d608eefb5643088c961e0e08

# Appendix - See Also

### General References

[https://guitarvydas.github.io/2021/12/15/References.html](https://guitarvydas.github.io/2021/12/15/References.html)

### Blogs
[blog](https://guitarvydas.github.io/)

[obsidian blogs](https://publish.obsidian.md/programmingsimplicity) (see blogs that begin with a date 202x-xx-xx-)
### Videos
[videos - programming simplicity playlist](https://www.youtube.com/@programmingsimplicity2980)
### Books
leanpub'ed (disclaimer: leanpub encourages publishing books before they are finalized - these books are WIPs)
[Programming Simplicity Takeaways, and, Programming Simplicity Broad Brush](https://leanpub.com/u/paul-tarvydas)
### Discord
[Programming Simplicity](https://discord.gg/Jjx62ypR) all welcome, I invite more discussion of these topics, esp. regarding Drawware and 0D
### Twitter
@paul_tarvydas
### Mastodon
(tbd, advice needed re. most appropriate server(s))

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
