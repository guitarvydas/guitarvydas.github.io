I believe that text-only programming languages negatively affect the ways that one can think about problems. In general, language affects thought. 

If you think only in terms of 1-in causing 1-out, everything looks like a function, even when functions aren't the best choice.  Like distributed computing, asynchronous processing, robotics, game programming, blockchain, internet, GUIs, daemons, servers, etc.  

The differences are subtle. 

For example, I used to build compilers, but, I don't bother anymore, I just build transpilers and whip up new languages in a fraction of the time that it used to take, e.g. hours instead of months. 

Text-only thinking subtly encourages synchrony, whereas diagrams encourage asynchrony. 

Using synchrony where it's not needed leads to bloatware and accidental complexity. 

Text-only thinking leads to poor design choices, like treating various happy paths as exceptions instead of treating them as valid parts of the design space. For example, imagine a lowly file chooser on an HTML page.  It has 4+ valid outcomes, not 1-happy-outcome-plus-exceptions.  The outcomes are: user abort (escape), file reader code failure, file doesn't exist, access privilege mismatches, OK, etc. Picking just one of these as being more important than the others leads to poor UX design and clumsy code. 

At one point in time, I designed electronics hardware using diagrams ("schematics"). That paradigm is much more flexible than writing software using one of the currently-popular programming languages (Python, Rust, etc). I would be able to guarantee that my hardware worked with zero (0) bugs when shipped, but, I would never put such a guarantee on any software.


# Appendix - See Also

### References

[https://guitarvydas.github.io/2004/01/06/References.html](https://guitarvydas.github.io/2024/01/06/References.html)

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
