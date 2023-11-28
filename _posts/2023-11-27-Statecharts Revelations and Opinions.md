# Revelations and Opinions About Statecharts

Harel's Statecharts offer wonderful insights into 
- diagrammatic programming
- isolation (encapsulation) of state
- isolation of control flow.

## DPLs Are First Steps Towards VPLs
Diagrammatic Programming is a form of VPL that uses only simple diagram figures and text.

For example, rectangles, ellipses, arrows, grouping, text blocks.  Stretchable.  Not arranged on a strict grid.

## Multiple Languages
In my opinion, you can't program an electronic machine using only *one* language.  You need to use multiple paradigms, hence, multiple languages.  

Physicists do this - they invent various notations based on "simplifying assumptions", express problems in those notations, then develop solutions to the problems in the same notations.  All the while, physicists remember what simplifications have been made and tend not to stretch the notations out of their sweet spots.  

I argue that we've stretched mathematical notation well out of its sweet spot in software development. I think that we need a new notation, probably more than one new notation, for programming. We need to admit to the reality of what is happening inside a programmable electronic machine (aka "computer") and then invent convenient "simplifying assumptions" to deal with pinpoint-targeted aspects of this reality. You cannot deal with the full reality in toto.  You can only deep-dive into aspects of the reality. A program should be composed of several sub-programs written in different languages. Most text-based programming languages are based on the model of assembler - top-to-bottom, left-to-right, step-wise sequencing of instructions displayed on a grid of non-overlapping cells. Programming - at the level of humans - doesn't need to be structured this way.  An example is relational languages, like Prolog. DPLs might allow us to break free of text-only thinking for programming language design.  Statecharts might inspire new DPL designs.  

I feel that Harel's Statecharts express control flow and event-handling better than any textual language I've encountered, e.g. Python, Javascript, Lisp, Prolog, Assembler, Haskell, Rust, etc.

Programming - broadly - consists of two activities:
1. inhale
2. exhale.


There is no fundamental need to use the same language (notation) for both activities.

In my mind, the question is not "how do I design one language to rule them all?", but, is, instead "how do I blend multiple languages together to create programs?".

## State Explosion Problem
I learned about state machines in EE school and thought that state machines were a good idea, but, that they suffered from the "state explosion problem". As soon as you build something "real" using state machines, the number of interactions and dependencies goes up exponentially making the result messy and non-understandable. 

Statecharts bring state machine notation to software development - and - solve the "state explosion problem" in a structured way. 

YACC and algorithms in the Dragon Book, also, solve the state explosion problem.  I like Harel's solution better and feel that it is more expressive.

Statecharts use the concept of *nesting* - imagine Russian Dolls - for taming control flow in software.  I have come to the conclusion that *nesting* is the holy grail of software development.  If you squint, you can see variations on *nesting* in DRY (Don't Repeat Yourself), in lambdas, in scoping, UNIX pipelines, structured programming, etc.  The antithesis of *nesting* causes problems with *global variables*, *memory leaks*, *dependencies* (explicit and hidden), *ad-hoc control flow*, etc.

## Parental Authority Instead of Inheritance
Statecharts do not use "inheritance" but use something that I call "parental authority" to apply structure to control flow.  

Inheritance makes sense for data structuring, but parental authority makes better sense for control flow structuring. 

With "inheritance", a method in a child (sub-class) can override the operation/meaning of a parent.  

With "parental authority", though, child methods cannot override methods in parents, hence, every piece of code makes stand-alone sense to the reader, without the need for the reader to dig through the dependency chain (static or dynamic) to understand what might happen.  

This can be seen in Fig. 2 of Harel's paper, where multiple events (written as "β") are abstracted into a single event controlled by the parent state.  The parent state is "D" in Fig. 2.  Sub-states "A" and "C" don't get a say on how "β" is to be handled.

## What Is An Event?
"Events" such as "β" are just blobs of data sent to *handlers*.  For example, a *handler* might be defined, loosely, as
```
function handler (self, message) {...}
```
At a minimum, a message is a *pair*
1. a tag
2. a lump of non-specific data

Of course, you can keep refining this notion with more detailed typing.  I've come to the conclusion that *messages* should be defined quite abstractly, letting the code inside the *handler* check for more specific details.  UNIX command pipelines are like that, except they define messages with too much detail.  UNIX pipeline *stdout* streams are defined as blobs of bytes, but, the byte `0x0A` is special. This built-in assumption makes it drop-dead easy to build text-manipulation commands in line-oriented ways, but, makes it less imaginable to do anything else.  In general, if you aren't encouraged to imagine something, you are likely to avoid it completely.  In UNIX, it is possible to build pipelines using generic binary data, but, it is easier to build pipelines of line-oriented commands.  That easy-ness tends to swamp out thinking about other arrangements and encourages text-only, line-oriented solutions.

The asynchronous-event abstraction allows for pipelines of type filters - each filter in a pipeline is asynchronous, and, checks for some type-ish property before passing the data further down the pipeline.  

This results in a *layered* approach to type checking, where the checks become tighter and more detailed as data travels through the pipeline.  We've seen hints of this concept in code that does "input validation" on web pages.

This, also, allows one to imagine checking beyond the simplistic concepts of type-checking.  EEs use the term "design rules".  Design rules encompass broader aspects of design problems encountered in  practical problem solutions, like cross-talk on printed circuit boards.  A design might look good on paper and on the workbench, but, when committed to a flat circuit board intended for mass production, it might be flaky.  Design rules to address such problems include constraints on trace length (thin wire lines of flat copper) versus spacing between such lines.  Other design rules might address equal line lengths with respect to the speed of light, e.g. two inputs to the same chip must ensure that electrons travel approximately the same distance before arriving at the chip, lest propagation delays come into play.

## Communicating State Machines
When I began thinking about communicating state machines, I immediately became unsatisfied with our current use of CALL/RETURN instructions.  CALL/RETURN instructions use global variables and mutation, even if you didn't ask for them. I naturally developed (discovered?) ways to apply structure to Message Passing, which I call Structured Message Passing and The Rule of 7.

In fact, EEs use communicating state machines and asynchronous operation as the default. Integrated circuits are inherently asynchronous.  Maybe that's why there is/was a Moore's Law for hardware, but, not for software?  Software programmers have come to loathe multi-tasking, EEs just accept it as a fact of life. This concept is so run-of-the-mill to EEs, that they don't even have a special name for the it. The difference, in my opinion, is how one starts out to address problems - do you assume that inherent synchrony is required, or, do you start out thinking that your problem space is composed of asynchronous elements and that you explicitly engineer synchronization into the few places that really need it?  

## Correctness, Failures In The Field
I got used to the idea that hardware I designed would have 0 (zero) defects in the field, whereas I never feel that way about my software designs. 

I need to build-in ways to fix and update my software. 

Does our current workflow, e.g. CI/CD, encourage the creation of buggy software?  Strong, static type-checking ensures some sort of correctness properties in programs, but, if the programs need to be updated, then, something is still wrong / unsatisfactory. Low levels of update activity on a repo might mean:
1. the code has been utterly abandoned
2. the code is near-perfect and doesn't need to be fixed.

Rhetorical question.  In the mid-1900s, Telecoms guaranteed "four nines" (99.99%) up-time for their equipment. When the power went out, the telephones still worked. The equipment was all programmed in assembler and C and other caveman programming technologies.  How did the Telecoms do this?  Would you put - at the risk of a lawsuit or jail time - such a guarantee on any of today's software, whether generated by human programmers or LLMs? Maybe the test for improved programming technologies should be our ability to extend the guarantees to five-nines?
# Appendix - Statecharts 
2023-11-27-Statecharts Papers We Love Video](https://guitarvydas.github.io/2023/11/27/Statecharts-Papers-We-Love-Video.html)
# Appendix - See Also

### References

[https://guitarvydas.github.io/2021/12/15/References.html](https://guitarvydas.github.io/2021/12/15/References.html)

### Blogs
[blog](https://guitarvydas.github.io/)

[obsidian blogs](https://publish.obsidian.md/programmingsimplicity) (see blogs that begin with a date 202x-xx-xx)
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

