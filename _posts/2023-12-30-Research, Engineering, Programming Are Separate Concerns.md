I have very strong opinions on this subject.

I think that Software Architecture, Software Engineering and Software Implementation are distinct classifications, with very different goals, requirements, and, legal implications.

Furthermore, I think that there are 2 fields of fruitful research:
1. The Science of Computation
2. The Science of Programmable Electronic Machines (PEMs).

Currently, emphasis seems to be heavily slanted towards (1) to the detriment of (2).  Even the name "computer" in "Computer Science" indicates a slant towards (1)-type belief systems.


1. Computistry
2. Pemics

Computistry is about forcing functional notation onto PEMs.  Computistry uses PEMs as tools, but, tends to avoid the full set of capabilities of PEMs, like sequencing. 

Pemics is about the Reality of programmable electronic machines, e.g.
- mutation
- single-threading
- etc.

A CPU is just a chip that contains a small amount of local memory, called "Registers", and some electronic logic that is used for interpreting and sequencing operations based on a "small" API, called "Opcodes" and some electronic logic that performs fundamental operations between locations in its local memory, e.g. Addition, Subtraction, Storing, Loading, primitive Sequence manipulation.

Pemics investigates the use of subroutines, whereas Computistry deals with idealized mathematical functions, which are not subroutines, but can be modelled with subroutines. Computistry forces the expression of computable functions onto the reality of PEMs by restricting the capabilities of PEMs, such as side-effects, time related functionality and forcing PEMs to perform operations which they were not designed for, e.g. concurrency, memory sharing, time-sharing, etc.

Pemics investigates the use of multiple notations for controlling PEMs, which include idealized mathematical functional notation along with other notations such as declarative exhaustive search notations, like Prolog, and, PEG, and, Diagrammatic Programming Languages, and, Visual Programming Languages, bloatware reduction, etc.

At times, Computistry uses its functional notation to delve into the description of PEM capabilities, such as with Denotational Semantics.  Computistry has evolved into a separate field of research which tends to veer away from describing the stark reality of PEMs and pushes aside various possible uses of PEMs, like sequencing.

Machine control theory *does* describe some PEM capabilities using the idealized functional notation of computistry, but, much of that can be replaced, in practice, by $0.20 worth of resistors, capacitors, coils, and functional equations based on continuous, rather than discrete, physics.  Such continuous equations were explored and developed and documented in the early days of electrical research by people like Tesla, Steinmetz, Wheatstone, Farraday, Ampere, Maxwell[^equations], and, others.

[equations]: Maxwell's Equations are regarded by some as the fundamental description of the full science of electricity, whereas, Maxwell's Equations only express a *slice* of electrical behaviour while suppressing the expression of other kinds of valid behaviours (such as self-induction).
# Cottage Industry vs. Engineering 
The term "cottage industry" is characterized by the fact that a single practitioner (or a team) "wears all of the hats" - design, implementation, testing, etc., etc. This kind of approach creates POCs (Proofs of Concept) and early versions of a product.  Cottage industry products appeal to innovators and early adopters.

Engineering, though, is the attempt to cubby-hole specific responsibilities and to assign sub-tasks to experts in each cubby-hole.  Engineering is an attempt to sub-divide an industry.

A "cottage industry" might also be characterized by the number of product defects that are experienced in the field.  Mature industries produce products that do not need to be upgraded and have no defects. The producer provides guarantees and defines boundaries within which the product will function without defects. Our legal system enforces such guarantees. Products that do not conform with their guarantees result in lawsuits or jail time.

# Waterfall Design
Static languages embody Waterfall Design methods - also known as dreaded premature optimization. 

If you write a program using a static language, then you are using the Waterfall method.  You think that you already know everything there is to know about a solution and you believe that you can code up appropriate data structures and operators to effect the solution without needing further exploration and iteration.  

When you Optimize an already-existing program using a static language, then you are engaged in Production Engineering, not Design. This is a reasonable approach - wait for the Design to stabilize, then Optimize it.

Writing a program from scratch using Production Engineering mentality is slow and snips off various degrees of freedom during Design.  Most popular programming languages encourage the approach of jumping into Production Engineering in lieu of doing Design first.

# Other Professions
Professions, other than computer programming, have adopted technical diagrams as media for expression of certain concepts, e.g.
- blueprints in structural Engineering
- schematics in Electrical Engineering
- diagrams of molecules and inter-atomic bonds in Chemistry.

Diagrams seem to be the language of Engineering.  Engineers hand off diagrams to Implementors.

A common adage is "a picture is worth a thousand words".  Engineers can pack a lot of thinking into a single diagram. Engineers hand-off such a diagram to Implementors.  Engineers don't need to deal with low-level details - that responsibility is handed off to Implementors.

Engineers bridge the gap between Architecture and Implementation.  Engineers think - deeply - about the intent of Architects' designs and fill in the missing technological gaps, making the solutions realizable using state-of-the-art, best-practices technologies. Implementors deal with the low-level issues for implementing and vetting the designs using specific technologies, e.g. programming languages, hardware logic families like TTL, etc.

Only after a design has been stabilized and realized, do Production Engineers refactor designs to make them more cost-efficient. In the software perspective, the difference in cost/speed/size of using an `int16` instead of an `int64` only matters after the design has stabilized and proven to be worth further development.  Until a Design has stabilized, use of more generic `int`s is appropriate in the software realization of various iterations of the Design.

# Myth - Software Engineers Must Use Programming Languages to Express Their Designs

Implementors need to use sequential programming languages to create scripts suitable for automatic interpretation by hardware.

Software Engineers need only communicate their ideas to Implementors.  Implementors need to worry about how to translate recipes from Engineers into machine-understandable scripts.

# Myth - DIY (Do It All Yourself)
The DIY attitude is OK for cottage industries.  One person *can* do everything.

For scaling projects up to larger teams of developers and to larger communities of users, the work needs to be divvied up.

"Thinking" is the hard part. Implementing (coding) is straight-forward and doesn't need to impinge on the Engineers' creative time.

We tried to "off-shore" the Implementation work, but, the only communication tools available to on-shore Engineers were programming languages.  Essentially, the Engineers did most of the Implementation work before off-shoring it.  Furthermore, our use of programming languages that use the callstack for implementing code libraries defies divvying up the work on libraries. The calling code is too dependent on the library code to make this approach fruitful. Code can't be off-shored because it has too many threads of dependencies running through it.

When you use a DIY approach, you can't divvy the work up and you're stuck with a *cottage industry* reality. Professions, such as accounting, had this problem until remote access technologies were promulgated.  Professional accountants were forced to do *all* of the work themselves, and couldn't scale their businesses upwards until they found a way to separate out the straight-forward tasks from the creative tasks.

# Appendix - References

[2022-09-19-Project Collaboration Jams](https://publish.obsidian.md/programmingsimplicity/2022-09-19-Project+Collaboration+Jams)

[2022-09-25-Clockwork Thinking Impedes Progress - as yet unpublished]


# Appendix - See Also

### References

[https://guitarvydas.github.io/2004/01/06/References.html](https://guitarvydas.github.io/2024/01/06/References.html)

### Blog
[blog](https://guitarvydas.github.io/)

### Blog
[obsidian blogs](https://publish.obsidian.md/programmingsimplicity) (see blogs that begin with a date 202x-xx-xx-)
### Videos
[videos - programming simplicity playlist](https://www.youtube.com/@programmingsimplicity2980)
### Books (WIP)
[leanpub](https://leanpub.com/u/paul-tarvydas)

### Pamphlets
[gumroad](https://tarvydas.gumroad.com/l/dvtej?_gl=1*o7hy6z*_ga*MjA0NzUyMDY1Mi4xNzA3NDc3MDIx*_ga_6LJN6D94N6*MTcwNzQ3NzAyMC4xLjEuMTcwNzQ3NzI5Ni4wLjAuMA)
### Discord
[Programming Simplicity](https://discord.gg/Jjx62ypR) all welcome, I invite more discussion of these topics, esp. regarding Drawware and 0D
### Twitter
@paul_tarvydas


<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
