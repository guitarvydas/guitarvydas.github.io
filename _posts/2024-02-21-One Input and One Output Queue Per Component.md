# One Input and One Output Queue Per Component
One output FIFO per box. The ports are "tags", not FIFOs themselves. Using only 1 queue provides time-relativity to messages. A FIFO is "homogenous" - it can contain messages with various types of content. The 1 queue gives messages an ordering-in-time, but not a type. (Typing can be done at a higher level, above the queue concept). This, in fact, goes to a different conversation - types are over-hyped. When you can see all of the ports, you don't need help in keeping the types distinct. Much like 7-line BASIC programs of old - it didn't matter if variables were global or not, what mattered is if you could SEE ALL of them at once [a lot of wasted brain-power went into sorting out the global-variable problem to preserve the insistence on using text, whereas the problem wouldn't have even have been a problem if, instead of text, closed figures (e.g. boxes) had been used instead of ASCII boxes (`{...}`). ASCII boxes allow leakage, closed boxes drawn on paper or whiteboard scream out - visually - when leakage occurs. Hence, the problem was deeper than the symptom called "global variables". We fixed the symptom (at great expense) but left the underlying problem in place (the problem is/was _containment_, and, it could be solved in more than one way, i.e. in the above diagram, it is "obvious" what is contained inside of what, but, writing this out in text makes it less obvious and open to tom-foolery by nerds])).


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
