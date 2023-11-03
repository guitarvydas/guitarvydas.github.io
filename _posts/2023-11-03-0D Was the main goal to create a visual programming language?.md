# 0D Was the main goal to create a visual programming language?

In this section, we delve into the core objectives that drove the development of a visual programming language. Initially, the main aim was to simplify the software development process by eliminating both explicit and concealed dependencies. This involved a thorough examination of the root causes and a shift away from the traditional callstack as the primary communication mechanism. Instead, the use of First-In-First-Out (FIFO) structures was adopted, a seemingly simple yet crucial change that was not immediately obvious.

Once all dependencies had been successfully purged, an intriguing outcome emerged: the creation of software diagrams became a natural byproduct of this approach. This was a paradigm shift from the conventional text-based coding methods, and it paved the way for a visual representation of software systems.

Historically, the primary motivation behind this endeavor was the creation of robust software, particularly at the driver level. The intent was to enable the development of drivers at a higher level of abstraction, replacing the ad-hoc C programming that was prevalent.

Furthermore, there was a belief that visual representations, such as diagrams, would yield more robust programs compared to their textual counterparts. This belief was substantiated by the success of various diagram notations, including Harel StateCharts and Electronic Engineering Computer-Aided Design (EE CAD), which demonstrated the effectiveness of visual approaches in various domains. In this context, the utilization of diagrammatic notations, like Drakon, held significant promise in achieving the overarching goal of software robustness.


# Appendix - ChatGPT Prompt
summarize the following markdown as a subsection for a chapter in a book
# Appendix - Point-Form Notes

- after doing it, then thinking about it, it turns out to be extremely simple - expunge all dependencies (explicit and hidden)
    - expunging dependencies 
        - understand causes
            - get rid of callstack as the primary communcation mechanism
                - use FIFOs, not LIFOs (easy to do, but, not obvious)
    - once you expunge all dependencies, diagrams of software come "for free"
- historically, the goal was to build robust software, esp. at the *driver* level
    - write drivers at some high level, instead of in ad-hoc C
- it was believed that diagrams or programs would be more robust than textual code for programs
    - example of successful diagram notation: Harel StateCharts
    - example of successful diagram notation: EE CAD
    - other examples
	    - Drakon

# Appendix - See Also

## See Also

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
