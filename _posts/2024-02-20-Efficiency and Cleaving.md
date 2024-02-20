FTR: I believe - strongly - that cleaving things apart is the "right thing". 

Plug-ins just cause epicycles down the road. 

An "editor" should edit, not check semantics / colourize / whatever. 

An editor should have an API that can be used by downstream components to feed commands back to the editor (colourization, dynamic flow display, changing pages, snapping to locations, etc.). Downstream components can check the validity of what is written then send commands back to the editor to flag errors (etc.). 

That's how compilers work - a lump of code does the "parsing", another lump of code does "the checking" and so on. 

When you conflate these issues, you cause accidental complexity (aka self-flagellation). 

Cleaving is "easy" and is the main thrust of 0D-ness. If you want to cleave something, don't use a function call, use a message send instead. 

Conflating issues like this is borne out of 1950s-style worryies about "efficiency". 

Instead, it's better to do the "right thing" and "efficiency" will come of its own, i.e. someone smart will figure out how to make it more "efficient". 

In fact, the meaning of "efficiency" has greatly changed since the 1950s, and may matter much less than it used to. There's also the question of "efficiency for whom? 
1. End-Users, or,
2. Developers?" 

The answers and techniques are quite different depending on who you're targeting. For example, developers can afford to use souped-up, but, expensive machines. Users want cheap machines. When targeting developers, you can afford to throw machine cycles away for the sake of development turn-around time. When targeting End-Users, you need to worry about speed and size, to reduce costs. 

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
