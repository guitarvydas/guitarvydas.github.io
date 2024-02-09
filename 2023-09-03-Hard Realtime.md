
I forced my children, when they were 5 years old, to learn a hard realtime notation.

Sam Aaron teaches multitasking to 10 year olds.

There is a Moore's Law for hardware, but, no equivalent Law for software. Why?

Concurrency is all around us, but, software scientists implicitly remove concurrency from their notation.  This notation then causes programmers to eschew concurrency and to treat concurrency as an edge case instead of begin front-and-center in all of their designs.

Software notation is based on *synchronous functions*.  This notation ignores concurrency.

Yet, concurrency is such a powerful concept that smart people have spent a great deal of effort in trying to create fake concurrency using synchronous notation.

I.E. a notation was invented to remove concurrency and to make every part of programming synchronous.  Then, this same synchronous notation was used to put concurrency back into programming.  I argue that this sounds like make-work.

I argue that thinking of electronic machines in *only* a synchronous manner deeply affects the way that programmers can *imagine* programming electronic machines.

## How Does Synchronous Function Notation Eschew Concurrency?

- all actions are described in terms of micro-steps
	- a micro-step is essentially a global, absolute clock
	- everything is tied together by a fine thread of small steps
	- when everything is tied together by fine steps, then nothing is truly independent
- ad-hoc blocking
- 1-in, 1-out, *always*
	- needed to add 2 outputs, by inventing the "exception" syntactical wart

## Other Words for Make-Work

- Accidental Complexity
- Epicycles
- Bloatware

insides of a CPU are asynchronous and essentially ad-hoc
- regularized by a *clock* that sequences stepping of the CPU machinery
- opcodes are the synchronous API of the underlying asynchronous CPU machinery

CPUs are stepped.  This does not mean that every notation we invent must, also, be stepped.  The notations merely need to be reduced to a sequence of steps, i.e. *compiled*.

Take, for example, Relational languages like PROLOG, miniKanren, etc.  Relational notation is not based on synchronous functions.  Relational notation may *look* like it's function-based, but it's not.  All of the clauses in the body of a rule must be true at the same time.  How to make the clauses true or how to determine if they are true is not specified by the notation.  At present, this detail - *how* - is left to the underlying implementation.  One could imagine *layers* of such implementations, each layer building on top of the layers below it.

I don't think that Relational notation is the epitome of all notations, but, it does show that it is possible to use a non-function-based notation for describing the operation of electronic machines - i.e. *programming*.

- need to express programming language in text --> synchronous form, left-to-right, top-to-bottom

- clocking - inserting a global clock - is used for designing APIs to ad-hoc asynchronous electronics

- local clock, not global clock
	- a single CPU uses a single clock for all of its API operations - opcodes
	- a single electronic device may include many CPUs, each with their own local clocks

https://en.wikipedia.org/wiki/Musical_notation


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
