- *VPLs as a concept have incredible potential*
	- We miss a huge swath of other possible concepts due to our indoctrination in function-based-only thinking.
	- What are some concepts that we miss out on?  
		- Think: anything that is considered "difficult" to fathom 
			- concurrency
				- thread-safety et al are unnecessary concerns
				- the true model of concurrency is: 1 CPU per thread
					- time-sharing was invented because CPUs were *very* expensive in the 1950s
					- memory management and GC was invented to conserve memory, which was *very* expensive in the 1950s
					- time-sharing, coupled with shared memory, causes lots of *gotchas*
						- e.g. "thread safety" is only a problem if you share memory
					- today, we have cheap Arduinos, rPis, etc. with lots of cheap memory
					- we can go back to using 1 CPU per thread instead of using time-sharing
						- this model *cannot* easily share memory, so thread safety is no longer a concern
							- all single-CPU threads are "safe"
					- CPUs, as originally designed, provided non-reentrant registers (instruction pointer, stack pointer, etc.) and non-reentrant, mutable RAM
			- libraries, snap-together components, LEGO-like software components
			- multiple inputs and multiple outputs
			- sequencing
			- daemons
			- mutation (a fact-of-life in CPU-based electronic machines)
			- deprecation of Operating Systems
				- preemption is a *trick* that makes function-based thinking work on sequential CPU-based machinery
				- the cost of preemption is high - bloatware, efficiency
			- deprecation of Textual Programming Languages
				- there is no fundamental need to treat CPU-based machinery in text-only form
				- CPU-based machinery can do more than can be expressed in text-only form
- *We have yet to find tools good enough for programming in them*
	- True, but it is possible to chip away at this problem.
	- Currently, I express diagrams using draw.io, then save the diagrams as text (XML) and parse the text using existing tools, then infer information and transpile to existing TPL form letting existing compilers do the heavy lifting.
	- Basic assumption - draw.io implementors know more about editing drawings than I do, they've been at it longer than I have
	- I have, also, used yEd, and, I think that Excalidraw will be fine for this purpose
	- My choice of using draw.io is "arbitrary" and driven by historical factors, I could have made other choices.
- *Architects should be able to express structures that, when zoomed out, are readable and understandable (... to visual programmers with some experience of the patterns, at least)*
	- taken literally, this is correct
	- the underlying theme is that there should be at least two programming languages - one for Architects and another for Implementors - "one-size-fits-all" only results in meh.
		- We used to think that creating languages was difficult, so we tried to create one-size-fits-all languages
		- Today, though, using PEG-based technologies and cheating by letting existing compilers do the heavy lifting, we can whip up multiple languages in only a few hours.  I call these kinds of things SCNs (Solution Centric Notations).
		- Many mature professional disciplines use diagrams instead of text for communication
			- e.g. EE schematics
			- e.g. EE state diagrams
			- e.g. atomic physic's Feynman Diagrams
			- e.g. material science visualization of molecular models
			- e.g. Chemistry's diagrams of molecules
			- e.g. Physic's diagrams of Atoms, Nuclei, etc.
			- e.g. Mech Eng CAD diagrams
			- e.g. Civil Engineering blueprints
			- etc.
- *As you zoom out on a system, the view should maintain a low total number of different objects you need to understand.* 
	- Yes, exactly.
	- You - the reader - should be allowed to choose how much detail you want to explore.
	- A cheesy way of "zooming out" is to use hyper-links to different web pages
		- Currently, I use hyper-links, mostly because the tools I use make this an easy choice
			- and, because I have been indoctrinated to think in terms of sheets of paper, non-zoomable
	- A machine cannot decide what a "low total number of different objects" is, the Architect must make this decision
		- "good architects" make the "right" decisions
		- "poor architects" make poor decisions regarding readability
		- what are the "right decisions"?  I'm not sure yet, but I know them when I see them
			- the test is that other people understand what I meant (they don't have to agree with me, they only need to understand why I did what I did)
		- the editing tool should help Architects by making it easy to elide information in layers without interrupting their thought processes
- *Sub-structures should appear as a single component/device, hiding their complexity.*
	- Q: what mark-up should Architects use to say "this is more important than that"?  What should be elided and what should not be elided as you zoom out?
	- Note that Architects might not have made the most-correct decisions
		- the most important thing is to *understand* what the Architect *intended*
		- then, you can argue with, and, learn from the design
		- perfection is not required, only understanding is required
	- markup - .md - gives us a guess at how to markup text, but, how do you markup diagrams?
		- I've been using line-width and opacity to help readability...
			- but, maybe, there are smarter ideas to be had?
		- maybe we need to ask professional Designers?
		- maybe visualization ain't the epitome of communication
			- what about sound?
			- movie studios use certain techniques
			- game designers use yet other techniques
			- what about evolvement over time?
		- IMO, "infinite canvas" models make it harder to comprehend a design than layered Rule-of-7 models
			- in essence, the Architect suggests how to read and understand the Design, instead of providing a wall of information on one flat sheet
- *We don't yet have decent theory or language for how to achieve better understandability*
	- Yes and No.
	- Schools of Design have better understanding of these issues than Schools of Programming do.
	- Schools of Programming produce experts in commanding machines.  Schools of Design produce experts in H2H communication (human to human).  Collaboration is needed.
	- It is self-aggrandizing folly to think that Programmers can understand H2H better than Designers.
	- Programmers want to communicate a tiny sliver of dense information - emotionless detail.  Not all Designers are cut out to communicate that kind of thing, but, the few that understand how to do that kind of communication can probably do it better than Programmers ever will.
	- example: today's games are developed by teams that include machine-command-techies and artists.
	- example: documentaries vs. artistic films vs. sitcoms vs. game shows vs. news shows vs. YouTube vs. etc.
		- there are experts in each genre


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
