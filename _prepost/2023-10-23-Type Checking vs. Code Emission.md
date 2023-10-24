
When it comes to textual programming, I conclude that we need a full-blown programming language for defining and manipulating and checking types.  And, another full-blown programming language for implementing code.  

In fact, if you think of type-checking as a Component (or a pipeline of Components), this breakdown begins to make obvious sense.  Some Components do type-checking.  The output of these Components is pipelined into Components that do code emission.  
![](/diagrams/2023-10-23-Type%20Checking%20vs.%20Code%20Emission%202023-10-23%2023.07.19.excalidraw.svg)


The emitter Components assume that the incoming code (intermediate code) is already perfect and type checked, which simplifies the task of figuring out what to emit and how to emit code.  

We already do this on the web - it's called "input validation".  

I sat through a reading of PLFA (Programming Language Foundations in Agda) and concluded that Agda was backing into these very concepts.  Agda, though, suffers from the one-size-fits-all meme and is a language for defining types with a language for doing implementation tacked on as an after-thought.

If an error is detected during type checking, or, during code emission, the input source is *not* passed on to the next pass, only an *abort* message is sent.


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
