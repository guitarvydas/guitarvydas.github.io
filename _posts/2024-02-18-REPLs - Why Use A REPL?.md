A program developer basically does two things
1. debug a Design for a program
2. ultra-optimize a Design that's known to be good, before putting it into production.

Our current crop of compiled languages tend to support activity #2 while ignoring activity #1 on the assumption that you never need to debug a Design. Or, debugging a Design takes significantly less time (10x less, say) than worrying about production engineering a Design.

It is possible to attack activity #1 by simply "thinking it through". On the other hand, it becomes much easier to fool around with a Design if a machine automates some of the process and augments your ability to iterate and to change your mind.  

When you change your mind, you don't just change the control flow through the program. You might, also, change the data structures. 

So, when you change your mind, do you simply make changes to your code and re-start the workflow from the top, i.e. re-compile and re-test?

My experience is that debugging a Design is a *lot* easier and a *lot* quicker when you use a REPL. A REPL-based programming IDE acts like a soup of program chunks and data chunks that you can replace and retry quickly (where "quickly" is measured in sub-seconds, not minutes). 

In fact, a REPL-based development environment changes the way you think, deeply changes what you think is possible, and, gives you more freedom to explore the design space.

When people dive directly into production engineering and skip lightly over design iteration, they are actually engaging in something called "Waterfall Design". They are so cock-sure that their design is perfect, or near-perfect, that they don't feel the need to debug it first.

Evidence suggests that design bugs happen *much* more often than we want to admit. So often, in fact, that we wasted valuable time inventing and using a tool technology called "Continuous Delivery". This tool allows program developers to punt on the act of debugging their designs, since they know that they are allowed to fix design bugs by fixing (called "upgrading") their code and shipping out new versions at the drop of a hat. In essence, they use customers as guinea pigs to help with design debugging - something that programmers should have done themselves first. Our culture has become convinced that bugginess is OK and that end-users should pay for the privilege of debugging designs, i.e. not sue the designer, not do the work for free, but, to actually *pay* for the privilege of using buggy designs.

Fixing code bugs and fixing design bugs are two very different things - we even use different names for the concepts ("bug fix" vs. "upgrade").

How can we improve the development workflow? Should we continue making type systems better and better for catching only a certain class of low-hanging fruit kinds of errors, leaving the issue of design debugging behind in the dust?  Or, can we improve the mostly over-looked issues of requirements gathering and design iteration?

Older languages, like Common Lisp, Smalltalk, etc., did begin addressing the issues of design iteration, but, that direction of research was nipped in the bud in lieu of over-emphasis on improving compilation and type-checking techniques.

Note that the issues of building a good REPL are more difficult than appears on the surface. For example, if you change your mind about the shape of data, what happens? A live REPL needs to track the location of every instance of that kind of data and to change all instances - in some way. Versions of Lisp that preceded the invention of Common Lisp did that. Smalltalk does that in simple way - methods are associated with OO classes, instead of being hard-wired and sprayed ad-hoc throughout the code base. 

Why not just do the big-bang thing - recompile afresh and re-load? This sounds good on the surface, but, we don't have evidence that it actually works. The turn-around is too slow and too clunky to encourage changing your mind quickly and easily. In fact, the effect of approaching the design problem in this way is so bad, that we had to waste time inventing CD technology to hide our failure to make this easier. And, our code has become wildly more bloated over the decades. Code bloat ain't because of so-called "essential complexity", it's because of the techniques we're using and the way that we measure "success". 

As Douglas Crockford says, if we could find a way to eliminate testing, it would be good. Type checking and static languages don't eliminate testing. Measured that way, one can only conclude that our current techniques, including type checking, are over-rated. 

Early languages, like Lisp, Smalltalk and others, provide a hint of how to reduce the cost of design iteration: interpretation and REPLs.

Note that *all* languages can be interpreted.  Only *some* of the languages can be compiled, though. We should be forced to use a compiler as only the last step in our workflow - i.e. when performing production engineering, or, better, by punting the work to Production Engineers who have a need for tight type checking and fine control of memory, but, only after a design has stabilized.

If a product needs to be upgraded, then its design is - obviously - unstable.

This idea of shipping only debugged designs is not far-fetched. EE's do it all of the time. Civil Engineers sign their name to their designs, with the threat of lawsuits or jail time. As far as I can tell, only software programmers get away with shipping buggy designs - basically snake oil.

In conclusion, I would say that you *need* to use a REPL at the front end of your workflow. Just insisting on having a REPL in your workflow will change the balance of decisions made by language designers and implementors. That would be a good start.


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
[gumroad](https://tarvydas.gumroad.com/l/dvtej?_gl=1*o7hy6z*_ga*MjA0NzUyMDY1Mi4xNzA3NDc3MDIx*_ga_6LJN6D94N6*MTcwNzQ3NzAyMC4xLjEuMTcwNzQ3NzI5Ni4wLjAuMA..)
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
