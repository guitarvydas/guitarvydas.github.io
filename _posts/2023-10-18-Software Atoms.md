
An *atom* is the smallest stand-alone unit that we *choose* to think about.

An *atom* is like a "line in the sand" - we *choose* not to discuss details below the atomic level and only *choose* to discuss compositions of these atoms, i.e. *molecules*.

Atoms are
- stand-alone
- composable
- asynchronous.

Function-based programs do not satisfy these criteria.

For example, user-defined functions only *appear* to be stand-alone, but, if they incorporate calls to other functions, they cannot stand alone without dragging the other function(s) into the mix.

User-defined functions *appear* to be composable, but the rules of composition are strongly defined by the underlying language.  Usually, the rules insist on sequential composition of lines of code and insist on an order of evaluation of arguments to functions, i.e. that all arguments must be evaluated before a function is invoked.

Functions are definitely not asynchronous, since a calling function must *block* until the callee returns a value.

## Work-Arounds

We have been trained to use workarounds - aka *epicycles* - that make functions appear to be atoms.



A low-level call, like `print(x)`, might be an *atom* if `print` is built into the underlying programming language.

On the other hand, a user-defined function, like `f(x)`, cannot be an atom


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
