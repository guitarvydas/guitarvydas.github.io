Raoul Duke posted this youtube link to PiLuD: [The Message Is The Medium - Douglas Crockford](https://www.youtube.com/watch?v=YD2tnHqNN7w)

I would agree with the idea that the "Actor model" makes programming orders of magnitude simpler.  

I think that FBP is simpler than what he talks about and 0D is even simpler.

I feel that a point is missed: a CPU, as originally designed, *is* an Actor capable of only single-threading.  Moore's Law has finally made it reasonable to think this way.  The stuff about data races and memory sharing and so-called concurrency, etc. is accidental complexity caused by a concern for cheaping-out - attempting to use fewer CPUs than the number of threads that are needed for a solution. 

Message-passing is fundamental, but, like GOTO, needs to be "structured".

How do you implement 0D with what you've got today?  FIFO queues, `send()` and `handle()` and a dispatcher. [refs to sample code available ... ]
## See Also
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
