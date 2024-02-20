Lack of readability and writability kills free thinking.

Options kill readability and readability.

We witnessed this effect during the transition from assembly programming to high-level language programming.

Early high-level languages put all arguments on the stack. This was - initially - quite inefficient.

Assembler programmers screamed that they needed finer control of register usage, i.e. more options.

Later, GCC proved the assembler programmers wrong.

Assembler programmers quit complaining and retired after GCC came out.  Programming languages that included syntax for *register* declarations and fine control of register usage, went away and were superseded by programming languages that presented fewer options and allowed programmers to think freely at higher levels.

# Normalization
Putting *all* args on the stack was *normalization*.

This standard way of passing arguments to subroutines looked inefficient at first. 

This normalization had at least two effects:
- it made it possible to create new higher level languages for human use
- it made it possible to write better optimizers in compilers - everything is the same, so writing code to optimize the normalized output of dumb compilers became easier to imagine.

UNIX also won big due to normalization. Until UNIX became popular, each peripheral device attached to a computer required special-case code to be written for it. UNIX's approach was to normalize access to devices - all devices were made to appear the same, they all looked like *files*. This normalization made it possible to write scripts that generalized to many devices. Generalized scripts made it possible to write more interesting, more complicated, scripts.


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
