I see Scheme and Racket as having 4th stage static type disease. Anything that has "classes" is symptomatic. 

Bizarrely, JS prototypes are better than CL classes, IMO. 

A symptom of the static-typing disease is the inability to provide a flexible REPL, like in a pre-CL lisp, or, probably Rebol, or Forth. I'm guessing that Janet suffers from this disease too, hence, my lack of eagerness to suffer trying to figure out how to install it. After sussing out how Justine Tunney's GC works, my patience for other languages has diminished greatly. 

I surmise that the way to make Sector Lisp useful is to find an adjunct language to use it with, without hacking on Sector Lisp directly. Kinda like the `save` button on a calculator. The calculation can be done using pure functions. The `save` button is *mutation*, something that doesn't belong in the domain of pure functional thinking. Trying to shove *mutation* into a purely functional language sullies the notion and causes a lot of inconvenient gotchas, accidental complexities, self-flagellation, work-arounds and epicycles.

In my mind, a language doesn't need to have one of everything. General-purpose languages are milque-toast. Bolting languages together is a better idea. For example, OhmJS is a great DSL for writing grammars, but lousy for doing most other things. Prolog is a great DSL for doing exhaustive search, but, painful for simply printing reports. Bolting OhmJS to JS is powerful. One could imagine yet more DSLs in the toolchain, avoiding all direct use of JS. 

UNIX® pipelines show us how to bolt languages together. Unfortunately, these ideas have been conflated with unrelated concepts and heavy-handed implementations. 

We can do better now. 

We know how to write *closures* without needing huge blobs of C code and MMUs, etc. We know how to build FIFOs which can be used as IPCs instead of the heavy-handed methods required by the use of processes and preemptive multitasking. We know how to build applications using lots of small bits of light-weight code ("functions" and "subroutines") that don't need MMUs nor fat closures (aka "processes"). The only thing preventing us from doing this is our psychological belief that we must use stack-based CALL/RETURN *only*. Adding closures and FIFOs to our toolchain doubles our set of choices for implementing applications.

"Static typing" is a prerequisite for "compiling", i.e. figuring out what can be culled to allow pre-compilation of some stuff. Example: most of JS can be pre-compiled, but `eval`ing of strings cannot be pre-compiled. The static-typing cult has decreed that you should use `eval` only once, at compile-time instead of using `eval` multiple times, at will, during run-time. "Compiler" == "eval". Languages that allow `eval` at run-time tend to be smaller and tend to include decent REPLs. 

The static-typing religion leaves Designers out in the cold. You can't easily just try things out, e.g. using a decent REPL. You have to pre-plan and pre-know what you're going to do, then use `eval` only once.  This is known as "The Waterfall Method".

Compilation is what you want when you do Production Engineering, but, not something you want when developing a Design.


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
