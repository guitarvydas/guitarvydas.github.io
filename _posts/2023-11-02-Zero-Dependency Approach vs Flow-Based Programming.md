### Back-Pressure

**Flow-Based Programming (FBP)** incorporates back-pressure and relies on the operating system for its implementation. This approach ensures that data flows smoothly through the system. 

In contrast, the **Zero-Dependency (0D)** approach doesn't inherently support back-pressure but instead uses ACK/NAK-like protocols, such as those used in networking. This approach doesn't require an operating system to handle back-pressure; instead, architects and programmers must explicitly implement it when necessary.  It is straight-forward to implement REQuest/RESPonse and ACK/NAK protocols in 0D.

### Input Queues

In FBP, there is typically one input queue per Port. This organization simplifies handling data flow between different components.

On the other hand, 0D employs one input queue per Component, which means that each Component is obligated to react to every input it receives. If a Component wants to defer processing an input, it must explicitly implement buffering.

### Output Queues
In 0D, Components cannot communicate directly with other components.

Components can *send* messages by leaving messages on their output queue.  The Component's Container routes messages from outputs to inputs when the Component finishes its work / reaction (much like a *yield*).

Each 0D Component has exactly one output queue.
### Concurrent Components

FBP requires operating system processes to support concurrency. It leverages the capabilities provided by the underlying operating system.

Conversely, the 0D approach offers a simpler implementation of concurrency that doesn't rely on the operating system. In this approach, a process is essentially a closure, simplifying concurrency management.

### Fan-Out

In FBP, fan-out is forbidden, meaning it is not supported as a concept. This limitation can have implications for system design and architecture.

In the 0D approach, fan-out is supported despite the technical challenges involved. Fan-out is considered essential for enabling abstraction in the system. It is seen as more of a user experience (UX) issue than a strict technical constraint.

## Appendix - ChatGPT Prompt
summarize the following markdown as a subsection for a chapter in a book
## Appendix - Point-Form Notes
### back-pressure
- FBP - yes
    - requires operating system
- 0D - no
    - back-pressure is just ACK/NAK-like protocol (e.g. networking)
        - doesn't require operating system
            - Architect / programmer must implement back-pressure explicitly (straight-forward

### input queues
- FBP - one queue per Port
- 0D - one queue per Component
    - Component must react to *every* input (Component has no choice)
        - if Component wishes to deal with the input later, it must explicitly implement bufferin

### concurrent components
- FBP - yes
    - requires operating system processes
- 0D - yes
    - simple implementation, doesn't need operating system
        - a *process* is just a *closure*, anyway

### fan-out
- FBP - forbidden
- 0D - supported, despite technical difficulties
    - fan-out is necessary for supporting *abstraction*
        - fan-out is a UX issue more than a technical issue


## Appendix - See Also

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
