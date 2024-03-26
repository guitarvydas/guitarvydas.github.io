"Computer Science" is no longer about REMs - Reprogrammable Electronic Machines.

CPUs were designed to be non-reentrant and single-threaded. 

"Computer Science" jumped the shark when it invented a way to force reentrancy onto non-reentrant CPUs.  

I would say that "Computer Science" is a sub-field of mathematics. It is exploring how to transform flat, written equations into quantized form, kinda like the idea of using FFTs to deal with analog signals in the digital domain.

As such, "Computer Science" is mostly about notation worship, maybe it should be called "Computing Science" or "Computistry".

The other field - the study of physical hardware - might be called "REMics". In earlier times, REMics studied how to build compilers, studied Denotational Semantics, how to describe CPU architectures in declarative ways, etc.

Mapping Computistry "functions" onto REMs does not result in better ways to use CPUs. It results in only *one* way to use REMs - within limits. We can observe these limits being hit when we try to deal with distributed systems, e.g. the internet.

Conflating the word "Computer" with lumps of hardware muddies the distinction between the two fields. REMs can do more than just compute functions. Computistry maps its techniques *onto* REMs, but, doesn't *define* REMs.

Furthermore, REMs in 1950 were vastly different from REMs in 2024. In 1950, CPUs were ridiculously expensive and memory was expensive and scarce. In 2024, CPUs are abundant and inexpensive, and, memory is abundant and inexpensive. The realities of 1950s REMs caused a bias in REMics towards wasting human time while preserving REM resources, spawning the field of Computistry. In 2024, the realities are completely flipped around - we should be wasting REM resources to preserve human time, but, we don't do that. We continue to apply 1950s techniques onto non-1950s hardware.

 All of the constraints and rules of Computistry  - e.g. no side-effects, assign-once, 1-in always results in 1-out, no mutation, etc. - lead to the ultimate goal of "referential transparency". This goal was achieved decades ago using various other means, such as "pin-compatibility" in EE, "macros", "compilers" (which are just text-to-text transformers), Microsoft Word's find-and-replace, etc. The attempts to force "referential transparency" *into* synchronous languages has caused decades of gotchas and workarounds involving ad-hoc band-aids. Workarounds used to be called "epicycles" in Galileo's time.

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
