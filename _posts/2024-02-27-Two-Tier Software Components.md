When building software using stand-alone layers, it helps to divvy components up into 2 broad classes
1) Containers, and,
2) Leaves. 

Containers are recursive and can contain components of type (1) or type (2). Leaves are bits of code that don't contain other components. 

Approaching the problem this way, instead of thinking that there is only one class of thing - "function" - makes it easier to solve the problem (of re-pluggability).

This is "necessary" but not sufficient. Lambdas achieve this kind of thing, but, insist on too many restrictions along the way. UNIX pipelines and networking are the closest thing we've got to pluggability. 

UNIX pipelines have 0D, but are restricted by text-based syntax and reliance on the special character `\n` and the baggage of being too closely associated with big fat operating systems and MMUs and other heavy-handed, inefficient concepts. We have tight small closures, we don't need processes and MMUs and preemption and ... 

Networking takes a different approach completely. Networking assumes that nodes have "free will" and define "protocols" between them, instead of assuming that nodes are tightly coupled and implicitly synchronized. Networking, though, carries the baggage of being associated with big systems with the assumption that it can't be done in-the-small. Re-routing a network is easy - just unplug ethernet cables and plug them back in with another configuration. 

Unstructured networking can create a rats' nest of jumbled interconnections. But, that can be (easily) solved, in a way similar to how "structured programming" solved the `GOTO` problem.

Another disconnect is the fact that most programming languages deal with how to program single nodes, whereas I see programming as more holistic - programming is a just way to construct something useful, starting with nano-networks and scaling upwards.

Leaves can use sync and fn calls internally, but they cannot communicate outwards other than by message passing. (Like in a UNIX process, the process must use IPC instead of function calls if it wants to communicate with another process).


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
