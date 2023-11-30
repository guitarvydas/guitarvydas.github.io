You're welcome to disagree with me, YMMV.  My take on software simplicity is...

- most simple: UNIX shell pipelines, Sector Lisp 
- least simple: anything from GNU, emacs

- I saw a lot of "simple" software in the 1970's (early games, early IDEs, )
- Sector Lisp
	- purer than pure FP, mutation not possible (no heap, either)
	- 2 types - Atoms and Lists
	- Sector Lisp is virtually useless on its own
		- although Woodrush has done some impressive things with it [Woodrush](https://woodrush.github.io) (like LambdaLisp)
	- I haven't checked out Tunney's other work, like BLC, Redbean, Cosmopolitan, Ape, but, I wouldn't be surprised if these were "simple", too
	- Sector Lisp is small because Tunney is doing something fundamentally right, not because it uses assembler tricks
- UNIX pipelines
	- wrap bits of software, snap them into pipelines like LEGO® blocks
- the other, more unfortunate, choice is: hack and add options
- define: "simplicity" 
	- simple for who?
		- end-user?
		- developer?
		- language designer?
		- mathematicians? 
		- academics?
- code libraries are NOT simple
	- but, programmers believe that code libraries are a good approximation to LEGO® blocks
	- complexity is due to hidden dependencies
	- "0D" is my way of decoupling code libraries, at a very low level
	- a CPU has a *single*, *shared* stack, so we have to play complex games with it to run more than one thread, which complexifies code libraries
- code, as we know it, is based on LIFO principles, as inspired by Assembler
	- Lisp is a programming language with a non-sequential textual syntax
	- Prolog and other relational languages and HTML (sans JavaScript) are examples of *declarative* textual syntaxes
- pipelines are based on FIFO principles (i.e. not LIFO, not stacks, not CALL/RETURN)
- the model for using "programmable electronic machines" has changed drastically since 1950
	- in 1950, CPUs and Memory were VERY expensive, 
		- so, it made sense to waste developers' time to invent ...
			- timesharing
			- Garbage Collection
			- Operating Systems
	- in 2023, CPUs and Memory are VERY cheap and abundant
		- the model of "concurrency" can revert back to the original model, i.e. one CPU plus private memory for each thread
		- time-sharing not needed
		- shared memory need not be supported by default
			- "thread safety", et al, just dissolves
				- "thread safety", et al, is just accidental complexity due to the misuse of the idea of sharing memory, thinking that this is necessary
		- Garbage Collection, except the Biblical Flood method, not needed
		- Operating Systems not needed
	- in 1950, hardware could only easily support non-overlapping grids of small bitmaps (aka "characters")
		- hence, in 1950, it made sense to develop text-only programming languages
		- text-only programming languages are "caveman IDEs" for programming
		- IBM channels, Apple Postscript printers supported "smart devices" with embedded, asynchronous electronic machines, but, ...
			- we went on a deep dive with single, *time-shared* CPUs and *shared* memory
			- this caused lots and lots of *gotchas* (a very public example was the Mars Pathfinder disaster)
	- in 2023, hardware can support vector graphics
		- cells can overlap
		- cells can be resized
		- sequential thinking is no longer needed
		- mice and keyboards and other input devices can be treated as asynchronous input devices and can be allocated one CPU chip + private memory for each kind of task
	- Functions in mathematics are *not* like subroutines in prEMs (aka "computers")
		- functions in math are more like "macros" - instantly swappable (no time penalties involved)
		- subroutines in prEMs are sequenced in time by CPU chips (which are just really fast interpreters)
			- this is *not* the same thing as "functions" in mathematical notation
			- hence, lots and lots of *gotchas* trying to work around the mismatches
		- subroutines are scripts, functions are macros - these are not the same concepts
			- forcing scripts and macros to be treated in the same way leads to accidental complexity, workarounds, complexity
	- software is always buggy in the field
		- hence, we invented support for bugginess, e.g. CI/CD and rapid updating
		- the measure for repos is backwards
			- lots of activity is bad
				- means that something needs to be fixed
					- if not the software itself, then the design
					- if the design is off, then it's a bug, regardless of whether the code implementing the buggy design is type-safe or not
	- hardware is often *not* buggy in the field (zero defects in the field)
		- chance of lawsuit for selling buggy products
		- chance of jail time for selling buggy products
	- Moore's Law for hardware
		- N.B. hardware is asynchronous by default
	- no Moore's Law for software
		- N.B. software is synchronous by default
	- my conclusions:
		- don't stretch paradigms
			- if you use FP, remove *all* semblance of mutation
				- no assignment
				- no heap
				- if this leaves you with a mostly useless notation, so be it
				- if this makes it impossible to fully solve a problem with a single notation, then, include another notation(s)
					- don't hack on the notation, just use/invent another notation
						- I've reached the conclusion that bloatware is due to our hacking on the FP paradigm, to add mutation and heaps to the paradigm
			- include other notations in a project if a given notation / programming language doesn't fit or is too restricted to solve the whole problem
			- solve problems in little bits (aka "divide and conquer"), using different languages
				- e.g Prolog supports exhaustive search, but was stretched to support formatting of output, resulting in accidental complexities and difficulty in writing simple code for formatted output, like, say, in JavaScript
				- e.g. JavaScript supports web page description, but was stretched to allow multitasking ("callbacks", promises, futures, ...), resulting in accidental complexities
		- "one language to rule them all" is a bad idea and can only lead to complexity
		- figure out how to plug different languages together
		- strong typing is good *inside* a software component, but bad for inter-component communication plumbing
			- comms needs to be dumbed down and use only a single type which is very low-level (e.g. `void *`)
		- build software in layers, with software LEGO® blocks (i.e. not code repos based on CALL/RETURN)
			- FIFO for comms, not LIFO for comms
		- eschew *options*
			- use wrappers and pipelines instead
		- eschew Operating Systems
		- eschew text-only programming languages
		- eschew synchronous-only programming
			- in many cases, you don't need synchronization, so, don't start out with a synchronous mindset
		- build progressive type pipelines instead of strongly typed languages
		- programs *became* non-simple when a whole program was no longer visible in one eye-full
			- the notation was stretched to allow "bigger" programs, instead of snapping little bits together in small, understandable layers
		- don't share memory by default
			- optimize only if necessary
		- optimization is the antithesis of scalability
			- most existing programming languages - Haskell, Python, JavaScript, Rust, etc. - force programmers to deal with optimization too early (like, right off the bat)
		- dynamic type checking should be the default, use static type checking sparingly only when optimization is proven to be necessary (e.g. by profiling)
		- prEMs ("computers" - programmable Electronic Machines) can do more than just act as automation of mathematics
		- projects that use current-day programming languages are essentially doomed to abandonment or complexification
			- every time you add a CALL to a subroutine, you are adding a hidden dependency, over time, this will result in complexity
			- regardless if the CALL is made indirect via "dependency injection" techniques
	
# Appendix - See Also

### References

[https://guitarvydas.github.io/2021/12/15/References.html](https://guitarvydas.github.io/2021/12/15/References.html)

### Blogs
[blog](https://guitarvydas.github.io/)

[obsidian blogs](https://publish.obsidian.md/programmingsimplicity) (see blogs that begin with a date 202x-xx-xx-)
### Videos
[videos - programming simplicity playlist](https://www.youtube.com/@programmingsimplicity2980)
### Books
leanpub'ed (disclaimer: leanpub encourages publishing books before they are finalized - these books are WIPs)
[Programming Simplicity Takeaways, and, Programming Simplicity Broad Brush](https://leanpub.com/u/paul-tarvydas)
### Discord
[Programming Simplicity](https://discord.gg/Jjx62ypR) all welcome, I invite more discussion of these topics, esp. regarding Drawware and 0D
### Twitter
@paul_tarvydas
### Mastodon
(tbd, advice needed re. most appropriate server(s))

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
