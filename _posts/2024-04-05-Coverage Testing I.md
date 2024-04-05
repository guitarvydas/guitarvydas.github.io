On my mind: we don't have a Type System that does away with all testing, yet. 

So, we should be thinking of ways to facilitate testing. 

I've had lots of success with "coverage testing". Simply create a small database that contains True/False for every branch point in the code (i.e. every function definition, every IF-THEN-ELSE, every WHILE loop, etc.). Create a battery of tests that crawls into every corner of the code. This works wonders for finding most bugs and dead code. 

In 0D, this would mean dynamically tracking every connection with a True/False. Spit out info in Prolog form, then use Prolog to query the runtime info and help tune testing. Hmm, this would be trivial to implement in 0D by hacking on the `get_component` and `route` subroutines. 

In other languages (say Javascript), this would be easy, too - use OhmJS to pre-process all source code and to automatically insert visitation memoizing. [IIRC, I did that on a compiler project, using a recursive descent parser (before PEG was invented)]


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
