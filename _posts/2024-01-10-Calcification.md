In my view, *the* problem is that lower levels of software become harder and harder to manage and more expensive to change. 

It behooves us not to gloss over it and not to accept it as a fact.

There are 2 parts to fixing a problem 
1. define / state the problem, then,
2. fix it. 

Method for identifying part 1: Ask "why?" over and over again, recursively. 

For example, first iteration: why are the lower levels more expensive to change?

An alternate way of asking the same question is "Why is/was there a Moore's Law for hardware but not for software?"

My current answer: deep asynchronousity, lack of dependencies. ICs are asynchronous, lines of code are synchronous. Computer "functions" are synchronous and create ad-hoc blocking[^preemption].  

[^preemption]: Ad-hoc blocking is battled by operating systems by using the sledge-hammer of *preemption*. 

Computer "functions" are subroutines, not mathematical functions[^macros].

[^macros]: Maybe the closest thing to mathematical functions in our programming languages, is the concept of *macros* in Lisp.

Computers are Programmable Electronic Machines (PEMs?), not solely meant for computation.

Paper is 2D. Computers are 4D (x/y/z/t). Using 2D equations to express 4D PEMics is a handy trick (physicists call this a "simplifying assumption") but cannot express the full breadth of 4D capabilities.  At a minimum, one needs multiple 2D notations to describe phenomena in 4D.

# Appendix - See Also

### References

[https://guitarvydas.github.io/2004/01/06/References.html](https://guitarvydas.github.io/2024/01/06/References.html)

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
