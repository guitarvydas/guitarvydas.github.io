A part of the problem in PEM Science (the Science of Programmable Electronic Machines) - that I obviously have not conquered - is to convince people that "VPL" does *not* mean "more of the same", and, that there are things that TPLs cannot - conveniently - express.  E.G. I can write FP code in assembler, but, I find it more convenient to use HLLs.  In fact, I know how to build and reconfigure electronic machines without using any programming language at all, but, I choose to use software.  Likewise, there are programming concepts that go beyond what can be conveniently expressed in TPLs.  

Example: currently we use "thread libraries" as *assembler* for creating distributed systems. TPL function calls to thread libraries and TPL syntax like "await" and "par" leaves lots to be desired.

The original problem dates back to the 1950s notion that we need to share memory, while in 2023, this is no longer required.  

To me, VPL means a *hybrid* of TPL and je ne sais quoi.  TPL isn't dead, but, it isn't the be-all-and-end-all.  There is some sort of calculus of meaning and aesthetics, that Raskin began chipping away at in The Humane Interface, that is separate from what we consider to be "programming languages" today.

As another example, how does one use Scratch to program the following very common pattern used in EE?  Is the result meaningful to another human reader, or, is it just meaningful to a machine, or, is it a milquetoast union of some features common to both?

![[notes 15 2023-12-11 14.42.37.excalidraw]]

N.B. the feedback loop is *not* recursion, because the + input changes in parallel and simultaneously to the - input, and, *time* is involved. Both inputs change at every step ; one input comes from the feedback, the other comes from the outside.  

*Functions* in mathematics are what programmers call *macros*, whereas in Reality, programmers are forced to use *subroutines*.  Iff you restrict *subroutines* enough and disregard the existence of *time*, you get something that approximates mathematical *functions*, with some *gotchas*. 

The key is not *that* one can express this diagram as text in a one-language-to-rule-them-all manner, but (a) *what it communicates* to the machine and (b) *what it communicates to another human*.  I conclude that you can't have both.  We already know how to communicate to a CPU-based machine - sequencing of *assembler opcodes*.  I argue that we need to concentrate on multiple notations that are meaningful to humans (e.g. whiteboard drawings) and how to transpile such notations into *sequences of assembler opcodes* and how to bolt a plethora of such notations together to form a final result, i.e. an electronic machine which does something useful.

In 2023, we are faced with a completely different Reality than that which existed in 1950. CPUs are, now, cheap and abundant.  Memory is abundant.  Internet, distributed programming, robotics, gaming, mobile telephones are being invented.  Yet, we continue to program like it's 1950.

Programming technocrats speak blithely of simplicity and robustness, but, the final results are anything but simple and robust after some 50 years of effort, as witnessed by:
- existence of CI/CD and frequent software updates
- lack of legal recourse for buggy software
- software shipped that has more than zero (0) defects in the field
- the fact that, to play Tetris, one has to pay big `$$$`s for a "computer" and has to pay tax to Microsoft or Apple, instead of just getting a Tetris promo freebie in the mailbox from their Real Estate Agent or walking into Radio Shack and buying, off the shelf, a Tetris hand-held for $7.99
- non-existence of a Moore's Law for software development.


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
