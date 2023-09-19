## CPUs are Not Computers
CPUs are electronic chips invented by electronics hardware manufacturers.  CPUs contain instructions named CALL and RETURN.  These instructions were *not* invented to support functions.  These instructions were invented to reduce the memory footprints of programs.  CALL and RETurn instructions are based on the notion of a single, shared callstack (a global, shared variable).  FORTRAN mimicked the use of these instructions to build memory-conserving code sequences that were - unfortunately - called "functions".  Originally, FORTRAN did not support recursion nor thread safety - i.e. just like CPU chips.  Later, it was decided that the concept of CPU "functions" should be the same as mathematical "functions". Programming languages were forced to support recursion (a mathematical principle, not a CPU principle).  

This misuse of CALL and RETurn caused - and is still causing - a number of kinds of accidental complexities.  

- CALL takes *time* - called *propagation delay*.  Mathematical functions do not take *time* and must be instantaneous for mathematics to work.  

- CPUs use global, shared data, e.g. *registers*, *mutable variables*, *RAM*, *SSDs*, etc.  Mathematics does not easily support the concept of global, shared data. 

- CPUs create side-effects.  Mathematics does not work in the presence of side-effects.  

These problems have been solved by notation worshippers via various contortions to their notations.

Even the name "computer" is a bad choice.  These things are Electronic Machines.  A secondary, but, very convenient property of EMs (Electronic Machines), is that they are easily programmable.  

I would suggest the use of the the acronym "pEM" instead of "computer" to continually remind us of what these things really are. 

Computer Science is no longer about *computers*, but, is about computing *using* pEMs.

Just to be clear, it was entirely possible to reprogram machines before pEMs were invented.  We could reprogram mechanical machines by machining new mechanical parts for them, and, we could reprogram EMs by rewiring them using soldering irons.  Reprogramming of pEMs is, though, quicker and easier than these earlier methods of reprogramming.  

Rapid reprogrammability leads to new ways to think about possibilities.  

I suspect that if we lift the yoke of thinking about computers as only overly-fancy calculators based only on functions, that we will find even more new ways to think about possibilities.  

pEMs. 

## Sequentialism
The religious belief in sequentialism has led us to believe that CPUs *are* computers.

It is believed that CPUs are computers are equivalent concepts.

As I argue elsewhere, computers are programmable electronic machines (pEMs).  

CPUs, though, are simply sequencer chips that are designed for single-threaded use.

Computers - better yet, pEMs - are collections of electronics of which only a portion consists of sequencing electronics.  pEMs contain electronics for displays, for keyboards, for storage, etc.

The idea of using function-based notations, like mathematics, is valid, but, is only part of the whole story.

## Concurrency, Async, Parallelism
The thing that is called *concurrency* is actually not asynchronicity.  

It is step-wise simultaneity.

"Asynchronous" means "not synchronous".  When all code is synchronized - as is done in most programming languages and operating systems - you cannot have asynchronicity.  

By definition.  

Code, currently, is synchronized.  The steps might be so small as to make it appear that processes are running asynchronously, but, they are not.

Do we have real asynchronousity today?  Yes.  Internet servers and clients.  Smart, portable phones.  Just about every human endeavour except programming, e.g. meetings at the office or online. 

How have we learned to deal with asynchronousity?  Protocols.  Do you start a meeting when not everyone has yet arrived?  Do you start a meeting when the main speaker has not yet arrived?  When you meet someone, do you shake their hand?

Programming languages have built-in synchronicity.  Execute this line of code, then execute the line of code that comes after it.  To call a function, evaluate all arguments first.  What if you don't want to evaluate an argument?  Invent a workaround (aka "epicycle") called Promises.

Treating *some* things as pure functions is a useful idea.  Treating *all* things as pure functions is over-kill and requires extra work.

Synchronizing *everything* was OK when CPUs were very expensive and we needed to invent workarounds to time-share CPUs.  

Today, though, CPUs are cheap and abundant.  

Synchronizing *everything* is no longer OK.

Programming languages that use deep-down, implicit, hard-wired synchronization and step-wise simultaneity are outdated and are not suitable for new-breed programming.

## The Big Red Reset Button?

So, am I advocating that we press the Reset Button?

No, we can preserve the advances that we've already made.

We might need to branch off. These things are programmable electronic machines, not just fancy calculators 

What do I mean?  I don't know yet, but, we've been exploring only a tiny slice of what these things are capable of.

## See Also
### Blogs
- https://publish.obsidian.md/programmingsimplicity (see blogs that begin with a date 202x-xx-xx-)
- https://guitarvydas.github.io/
### Videos
https://www.youtube.com/@programmingsimplicity2980
### Books
leanpub'ed (disclaimer: leanpub encourages publishing books before they are finalized)
https://leanpub.com/u/paul-tarvydas
### Discord
https://discord.gg/Jjx62ypR  ("programming simplicity") all welcome, I invite more discussion of these topics
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
