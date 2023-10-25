
I see that https://ntrs.nasa.gov/citations/20230012154 classifies the Mars Pathfinder disaster as a coding/logic problem.

I see it more as a religious problem.

The religion is that of deeply believing that every programming problem can be solved by applying function-based, synchronous thinking, augmented by ever-more-complicated type checking.  Religious zealots believe that this approach will remove all need for testing and remove all forms of ad-hoc design.  Clearly, this was not the case in the Mars Pathfinder disaster.

IMO, the Mars Pathfinder problem was caused by the over-removal of asynchrony - true concurrency - from the problem and replacing it by step-wise simultaneity, then mis-labelling this approach as "concurrency". This led to the problem that Facts were ignored.  The bug was encountered - apparently "randomly" - before launch, but, ignored.  The use of the function-based, overly-synchronous paradigm caused an unforeseen *gotcha*, but, it looked liked a random Act of God, and was, thus, ignored.

The "problem" was solved by gluing an ad-hoc solution - called "priority inheritance" - onto the function-based, synchronous meme to force that single meme to continue working in that domain - well away from the meme's *sweet spot*.  These kinds of fixes - ignoring reality and forcefully "fixing" them - were called "epicycles" in Copernicus' day.

Today, so-called "computer science" is not a science *about* computers, it is a science *about* how to use computers to solve one narrow problem - computation.  Not all problems in Reality can be reduced to straight-forward *computational problems*.  

We live with true concurrency every day.  

For example, we hold meetings at work involving many asynchronous components - people - and, we have developed protocols on how to deal with late arrivals of attendees and different protocols on how to deal with late arrivals of principals, e.g. presenters and CEOs.  Everyone - except programmers - inherently knows how to deal with asynchronicity.

For example, hard-realtime notation and implementation is not considered a problem for 5 year olds ("music lessons"), but, hard-realtime is, seemingly, a problem for programmers when the wrong meme is employed, i.e. a function-based, overly-synchronous approach.

Today, most programmers believe that the CALL opcode was invented to support *functions*.  This is not the case.  CALL was invented to reduce code size and memory footprint on a single kind of single-threaded sequencing chip, called a "CPU".  FORTRAN applied the CALL instruction to subroutines.  Subroutines later became converted to functions.  Functions on clay tablets and papyrus don't work like CALL/RETURN works in CPUs.  You can fake it, but, eventually the fakery comes back to bite you, especially if your forget that mapping functions onto CALL/RETURN with shared, mutable registers and shared, mutable memory was just a simplifying assumption.

Today, the over-use of a single, function-based, synchronous meme is causing much more memetic damage than is recognized.

For example, today most programmers think that *programming* consists of the act of sequentially arranging non-overlapping cells of fixed-sized bitmaps on strict grids using something called a "programming editor".  Programming really is just: making a machine, based on changeable electronics, do what is intended by the engineers. Then, getting the engineers' ideas about what should be intended to match up with users' ideas of what is actually needed.

The memetic damage influenced by this single function-based, synchronous meme, causes programmers to avoid whole swaths of different approaches to solving problems, e.g. diagrammatic programming, true concurrency, multiple CPUs, "creativity", etc.

Religious zealotry makes it *look* like these other approaches are more difficult, when, in fact, they are easy when one avoids the one-size-fits-all approach to problem solving.


## See Also
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
