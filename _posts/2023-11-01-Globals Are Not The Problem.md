
In this subsection, we explore a significant challenge in software development - the issue of global variables and information structure. Global variables themselves are not the primary problem, but, rather, the problem is the way that globals affect our ability to understand and manage complex programs. This challenge becomes more apparent as programs grow in size and complexity.

In the past, when programs were relatively small, the presence of global variables was manageable. For example, in short 5-line BASIC programs or small snippets of Assembly code, it was relatively easy to keep track of variables. However, as software projects have become larger and more intricate, unstructured leaking of information, that I refer to as "spaghetti data," has become a common issue.

One way to address this problem is by emphasizing the importance of making everything explicit. Denotational Semantics is a discipline that has tackled this problem by insisting on explicit representation of everything, including control flow. In contrast, modern programming languages tend to make control flow implicit, which can lead to challenges in understanding and managing complex code.

To address this issue, we need to introduce the concept of "Ports." Ports act as channels for structured communication. For example, parameters to functions (aka lambdas) can be thought of as cave-man Ports, providing a structured way for functions to receive data. In more complex scenarios, processes communicate using mailboxes, which are also  Ports. However, mailboxes are often unstructured, leading to challenges in maintaining information flow.

To overcome this, developers should focus on Structured Message Passing, a practice that enforces a more organized and explicit way of transmitting data between different parts of a program. By addressing the problem of information structure, we can enhance our ability to manage and comprehend large software systems.

## Appendix - Meta-Discussion What's Going On Here?

I wrote this essay in only a few minutes (about 30 minutes) using a set of point-form notes then asking ChatGPT to convert the points into fleshed-out prose.

At present, I need to do all this manually
1. create notes in Kinopio
2. rewrite the notes in markdown format
3. poke the markdown into ChatGPT with an appropriate prompt
4. lightly edit the results.

I want a tool(s) that automates some of the steps[^tool].

[^tool]: I have begun working on such a tool, but, work could proceed more quickly, esp. if someone else were doing it. https://guitarvydas.github.io/2023/10/29/Experimenting-With-ChatGPT-As-My-Ghost-Writer.html

The following Appendices contain most of the bits of this work, that led up to this essay.

## Appendix - Original Notes in Kinopio

![Kinopio](/diagrams/2023-11-01-Globals Are Not The Problem Screenshot 2023-11-01 at 5.52.22 AM.png)
## Appendix - Point Form Notes as Markdown

Global Variables are not the problem
- the problem is...
	- you can't see all of the variables in one eyeful
		- this wan't a problem when programs were "small"
			- e.g. 5-line BASIC programs
			- e.g. small snippets of Assembler
	- unstructured leaking of information
		- I would call this *spaghetti data* while others call it *global variables*.
		- Denotational Semantics
			- solved this problem by insisting on making *everything* explicit
			- *everything* - includes *control flow*
			- modern languages make control flow implicit
				- top-down implied
				- left-to-right implied
				- CALL/RETURN stack is not visualized
		- need Ports
			- *Lambda* parameters are cave-man Ports
			- mailboxes for processes are Ports
				- mailboxes are *unstructured*
					- need Structured Message Passing

## Appendix - ChatGPT Prompt

The prompt to ChatGPT was "summarize the following markdown as a subsection for a chapter in a book".

When it complained that I had not supplied the markdown, I pasted the above markdown into the prompt input box.

## Appendix - See Also

### References

https://guitarvydas.github.io/2021/12/15/References.html

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
