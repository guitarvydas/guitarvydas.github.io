I believe that `IF-THEN-ELSE` is too low-level and too ad-hoc. 

`IF-THEN-ELSE` grew out of `COND` which was intended to represent conditional values of functions.

Programmers, though, extend the use of `IF-THEN-ELSE` by coupling it with variables to create ad-hoc, custom control-flow constructs.

The emergence of various *map()* functions and case-ing based on *pattern-matching* is a workaround for incrementally replacing use-cases of `IF-THEN-ELSE`.

Let's just go all the way. Let's use *parsers* to provide syntactic *pattern-matching*. That's probably expressive enough. If not, we can add *semantic* and *type-based* *pattern-matching*.

Replace control-flow uses of `IF-THEN-ELSE` by a parse. Leave `COND` alone, for determining conditional values of functions, but, not for control flow. 

Historically, it's been a tough slog to build parsers, but, OhmJS (and PEG) make this task massively easier. 

# Appendix - The Power of Ohm and PEG
see 2024-04-06-The Power of Ohm and PEG

# Appendix - See Also

### References

[https://guitarvydas.github.io/2004/01/06/References.html](https://guitarvydas.github.io/2024/01/06/References.html)

### Blog
[blog](https://guitarvydas.github.io/)

### Blog
[obsidian blogs](https://publish.obsidian.md/programmingsimplicity) (see blogs that begin with a date 202x-xx-xx-)
### Videos
[videos - programming simplicity playlist](https://www.youtube.com/@programmingsimplicity2980)
### Pamphlets
[DSL for Writing DSLs](https://tarvydas.gumroad.com/l/hiypq?_gl=1*1bdn1r0*_ga*NTI5MDkzNTI0LjE3MTAzNTQzNjU.*_ga_6LJN6D94N6*MTcxMTQ4ODE0Mi43LjAuMTcxMTQ4ODE0Mi4wLjAuMA..)

[Is Concurrency Difficult?](https://tarvydas.gumroad.com/l/dvtej?_gl=1*o7hy6z*_ga*MjA0NzUyMDY1Mi4xNzA3NDc3MDIx*_ga_6LJN6D94N6*MTcwNzQ3NzAyMC4xLjEuMTcwNzQ3NzI5Ni4wLjAuMA..)
### Discord
[Programming Simplicity](https://discord.gg/Jjx62ypR) all welcome, I invite more discussion of these topics, esp. regarding Drawware and 0D
### Twitter
@paul_tarvydas
### Books (WIP)
[leanpub](https://leanpub.com/u/paul-tarvydas)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
