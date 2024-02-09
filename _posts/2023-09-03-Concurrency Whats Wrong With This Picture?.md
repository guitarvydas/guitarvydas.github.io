
If you've every used a control-key on your QWERTY keyboard or played a 3-finger chord on a piano, you've used concurrency.

If you've ever sat in a meeting at the office or on Zoom with one person in charge - that's synchronization of a bunch of concurrent people.

Concurrency is all around us.  We use concurrency, and, take concurrency for granted, thousands of times a day.

Sam Aaron teaches concurrency to 10 year olds[^sonicpi].

[^sonicpi]: https://www.youtube.com/watch?v=TK1mBqKvIyU&t=10s .

Control-S is not two (2) keys pressed at the same time, it's either
- the Control key pressed, then, a short time later, the S key pressed,
- or, the S key pressed, then, a short time later, the Control key pressed. 

The 2-key chord makes it *seem* that the two keys are pressed simultaneously.  The only reason that it *looks* simultaneous is that we cannot perceive time differences that are very short.  Computers can perceive such small differences in time, but, we can't.

In 1975, I could program a concurrent QWERTY keyboard to handle control-keys, using Assembler.

In 2023, can I use Python, or Rust, or Haskell to do this same low-level task more simply and at at higher level?  

No.

What's wrong with this picture?  

45+ years later and it ain't gotten any easier or more robust.  

I argue that we can have a programming language that can address lower-level as well as higher level issues and does not need to rely on Assembler-written low-level code as much.

I had my nose rubbed in this problem at my first real job in 1981 (Mitel Corp.) when I couldn't get an MC6809 to keep up with a 9600 baud RS232 line, when using a thread library.

I could design *hardware* doo-dads that worked with zero (0) defects in the field[^defects], but, I have never been able to do that with *software*.

[^defects:] That doesn't say that the design had zero defects, only that, after bench-testing, the shipped product had zero defects. The end-user never got to see the defects that I saw before shipping. The end-user was not treated as my free Q/A department. In fact, the end-user could sue me in a law court, or have lemon-laws passed against my products, if my product failed to deliver on its claims.

What's wrong with this picture? 

Hardware had Moore's Law.  Software didn't.

What's wrong with this picture? 

That's an interesting question.

Why?

As far as I can tell, the difference is in mindset.

In hardware, every chip is asynchronous, concurrent, by default.

If you want synchronous behaviour in a hardware design, you have to put synchronicity in explicitly.

In software, no piece of code is asynchronous by default.  Everything defaults to being synchronous due to our reliance on function-based programming.  By "function-based", I mean a programming language that uses functions.  Not just FP (Functional Programming), but FORTRAN, C, Rust, Python, etc., etc.

This everything-is-synchronous-by-default mindset affects the way programmers think about problems and causes them to overlook different (smaller, more understandable) solutions to many problems.  In fact, what is called "async" today, is really asynchronous code built on top of a substrate composed of synchronous code[async].

[^async]: In fact, ironically, it is asynchronous code built on top of a substrate of synchronous code built on top of a substrate of asynchronous behaviour.

Hardware designers, on the other hand, start out with an everything-is-asynchronous-by-default mindset when solving problems.

A subtle difference with huge effects.

Just about every programming language that I know about is function-based.  The exception is the class of relational languages, e.g. PROLOG, miniKanren, etc.  Well, and HTML.

Functions affect thinking in several obvious way.  More importantly, functions affect thinking in several unobvious ways:
- Functions imply ad-hoc blocking. The caller suspends operation until the callee returns a result.
- Functions imply a strict routing policy. The callee *must* return a result to the caller instead of choosing where to send information.
- Functions encourage the use of name-coupling.
- Function-based thinking gives programmers the warm-and-fuzzy feeling that they no longer need to worry about UX issues.

Name-coupling can be solved by indirection.  DLLs were invented for this purpose, but, DLLs only do 1/2 of the job.  DLLs decouple the call, but don't decouple the return nor get rid of the strict routing policy.  Dependency injection adds indirection, a kind-of roll-your-own DLL strategy.  Dependency injection has the same problem as DLLs when it comes to decoupling the global call-chain record called the callstack, nor does it solve the strict routing policy problem.

Ad-hoc blocking can be solved by inserting extra software to force preemption and to swap stacks.  This extra software is usually called "operating systems".  

Users don't really need operating systems, but, they use operating systems because programmers give them buggy software that needs to be preempted and preventatively-rebooted.  This costs users money ($) and hardware footprints and memory footprints that could be used for other purposes.  The gaming industry invented a perfectly reasonable alternative to using operating systems - the game console and game cartridges.

Yes, users also want the other thing that operating systems provide - libraries of device drivers for their peripherals, e.g. printers from various companies, keyboards, mice, etc.  Unfortunately, the libraries tend to be written in function-based programming languages and, therefore, tend to be bigger and less-pluggable than would be expected[^bottleneck].

[^bottleneck]: https://guitarvydas.github.io/2020/12/25/The-ALGOL-Bottleneck.html

Software developers want preemptive operating systems when they work on buggy software.  Unfortunately, developers have come to rely too much on preemptive operating systems and use them as an excuse to ship buggy software.  The whole CI/CD culture is built around fixing bugs and doing upgrades *after* an app has shipped.

# How to Break Free of Functions
My suggestion for breaking free of function-based thinking is to build islands of code.  

Call functions that are only within the same island. 

To invoke functionality that exists on other islands, send messages.

This isn't hard to do, but it isn't the first thing that programmers think of when using function-based languages.  

The fact that programmers are encouraged to think only one way - to use functions by default - causes them to solve problems in only one way.  It is *possible* to send messages using function-based languages, but, it looks like extra work and is avoided at first glance.  Additionally most of our formalisms are based on the idea of tightly coupled, synchronous devices, so programmers get little help in thinking outside of that box.

Another way to break free of functions is to use notations that aren't based on functions, like relational languages.

Another way to break free of functions is to use anything-but-text when thinking about problems. Diagrams, on napkins, on whiteboards, etc. don't impose a pre-determined regimen on one's thoughts.  In the end, if you want to use a CPU chip, then you will have to map your thoughts onto a synchronous, step-based architecture, but, you don't need to commit to that paradigm until the end of your design cycle.  There is no reason to pollute your design-thinking with optimization-thinking.  In fact, designing takes longer when design-thinking and optimization-thinking are conflated.  We have powerful electronic machines at our disposal - why don't we use these machines to do the mapping for us?  Instead we are forced to explicitly do the mapping to a step-based architecture, manually.

# Appendix - Notes
- CPUs are just chips, CPUs are not computers
	- In the 1950s, you were allowed to use only one (1) CPU and you had to figure out how to time-share it.
	- In 2023, you have bowls full of CPUs to use, in the form of cheap Arduinos, rPIs, laptops, phones, etc. - time-sharing is outdated.  Robots, automobiles, even childrens' toys are rife with CPUs.
- Software is just soft hardware, you can reprogram electronic hardware using wires and soldering irons, but, software is a faster way to reprogram electronic machines.
- A *process* is just a closure.
- A message queue is just a FIFO.
- CALL/RETURN is not based on FIFOs, CALL/RETURN is based on LIFOs.
- CALL/RETURN was not designed to support functions. CALL/RETURN was designed to reduce code size at the expense of runtime speed (a CALL and RETURN takes extra time)
- CPU chips insist on providing global, shared resources, i.e. registers, a single callstack, etc.
- CPU chips were not designed to support multi-threading, CPUs were designed to support single-threading.
- Multi-threading within the same CPU requires extra software.
- Multi-threading within the same CPU was a way to time-share and optimize the number of CPUs needed for a design. Time-sharing is outdated.  But, time-shared multi-tasking continues to be pervasive.
- The original model of multi-threading was based on the notion of sharing memory and sharing CPU power.
	- Concerns about sharing CPUs are, now, outdated.
	- Concerns about sharing memory are, now, outdated.
- The "true" model of multi-threading is the idea of using multiple CPUs with no memory sharing, you don't need all of the extra software and complexity that we get using, say, Linux, to fake out this "true" model of multi-threading.  If, that is, you *need* to fake out multi-threading at all.
- Time-sharing and memory-sharing brings a lot of baggage ("gotchas", inefficiencies) that we don't need any more.
- Function-based thinking was invented for expressing mathematics on papyrus and clay tablets. We can do better now, since we have 4D media. Electronic machines can display four (4) dimensions x, y, z, t.  The newer 4D media can replace paper-and-pencil media.
- CPU means "Central Processing Unit".  We want to be thinking about DPUs now ("Distributed Processing Units").  The internet is distributed, blockchain is distributed, iPhones are distributed, robot limbs are distributed, etc., etc.
- Looping, recursion, calling functions, etc., are operations that don't make much sense in a distributed environment.
- We need languages for creating programmable electronic machines composed of distributed nodes, instead of more languages for programming single nodes.
- "Computer Science" is not about programming electronic machines.  "Computer Science" is about using programmable electronic machines to perform computation.  The idea of using programmable electronic machines to do other things - like sequencing - is mostly ignored.
- ChatGPT is trained on synchronous programs.  ChatGPT can interpolate, but cannot reliably extrapolate.  Hence, ChatGPT is not the ideal vehicle for creating distributed computers.
- Languages are very much easier to design today, than they were back in 1950.  We can build many little languages, geared towards our problem, instead of using General Purpose programming Languages.  PEG, and the variant called Ohm-JS, make it much easier to build new syntaxes in only a few hours, compared to days/months/years for building new languages using CFG-based approaches.  We now have many very-hot compilers and compiler technologies and toolbox languages, so we don't need to do much heavy lifting any more.  We can freely invent new syntaxes and wrap them over toolbox languages.


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
