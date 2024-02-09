Q: What is a *spaghetti program*?

A: Any program that is not fully nested in a manner 

- Russian dolls
- how to create spaghetti control flow?
	- conflate control flow with data
	- use IF...THEN...ELSE conflated with non-local variables
		- IF...THEN...ELSE is too low level - invent better syntaxes for conditional use-cases
			- e.g. CASE on TYPE is OOP method calling (conditional control flow without explicit IF...THEN...ELSE)
		- IF...THEN...ELSE was invented to handle conditional function values, not control flow, called COND in McCarthy's Lisp 1.5
	- allow hidden control flow dependencies
	- use CALL/RETURN in clever ways
		- CALL/RETURN was not invented to support functions
			- it was invented to save code space
- Drakon tutorials for pure control flow, structured
- Structured Programming 
	- localized, only, nesting of control flow for synchronous programs
- Lambdas 
	- attempt at localizing / nesting data
	- free-for-all for control flow - function calling is not guaranteed to be nested
- Packages
	- greasy attempt to nest names - knee-jerk band-aid instead of fixing true problems
	- nests names, but not control flow
- 0D
	- nesting of control flow - isolation of control flow
	- step 1 - isolate nodes
	- step 2 - nested architecture (Structured Message Passing)
- Structured Message Passing
	- nesting / layering of message passing architecture
- CALL RETURN Spaghetti



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
