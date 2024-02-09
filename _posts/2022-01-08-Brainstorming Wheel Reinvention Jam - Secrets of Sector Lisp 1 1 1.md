[This essay is a set of thoughts for an upcoming Jam. In the end, I worked on something else.]
# Secrets of Sector Lisp vs Wheel Reinvention Jam
- Goal: understand the secrets of Sector Lisp
- Implementing: implement SL as an embedded language (for C++?)
- Collaborators: open, 

# Discussion
- Sector Lisp
	- the whole language fits in under 512 bytes
		- [sic] bytes, not K, not M, not G
	- Garbage Collection in 40 bytes
		- how is this possible?
	- J. Tunney created this version of GC
		- this GC is not McCarthy's original GC
	- after 50-70 years of banging our heads on programming fads, Sector Lisp (based on McCarthy's original Lisp) is Orders of Magnitude smaller than any programming language
			- why?  
			- I believe that this smallness cannot be attributed only to assembler tricks, there must be something deeper at work
				- what is this "Je ne sais quoi"?
				- can we apply these secrets to other programs and programming languages?
				- will this lead to a better understanding of the reasons for "code bloat"?
	- create Sector Lisp implemented in Ohm-JS 
		- transpile SL to SL
		- transpile SL to  C/C++
		- ostensibly: create a Sector Lisp Embeddable Language
	- changing our mind: we will follow the path of least resistance, wherever that takes us
	- taste: *previous notes* [TBD]
	- collaborators:
		- no experience necessary
		- I hope to impart how to use Ohm-JS to collaborators
			- thinking "macros" instead of "compilers"
			- *toolbox* languages, don't re-invent compilation, use existing compilers to do the heavy lifting
			- YAGNI approach to programming
		- SL is quite simple
			- implementing SL should take only a few hours, 
			- but, understanding *why* SL is small might take longer, I dunno
	- First Principles Thinking
		- https://fs.blog/first-principles/
		- what *first principles* are at work here?



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
