# Three Classes of Types
1. Statically checked
2. Dynamically checked
3. Unchecked

# Examples
## Statically Checked
What we tend to call *type checking*.

*int*, *float*, *double*, etc. - i.e. enough bit-level detail that can be checked and peeled off by a preprocessor (most often called a *compiler*)

*Classes*, *structs*, etc. 

- *Odin*
- *Haskell*
- *Rust*
- *Racket*
- *Common Lisp* when type annotations are used
- etc.
## Dynamically Checked
- duck typing
- Odin's *any*
- unions
- often implemented by references
- often use GC (Garbage Collection)
- Lisp-style dynamic typing where the procedures check - at runtime - the datatype before performing an operation
- *Python*
- *JavaScript*
- *Smalltalk*
- *Lisp*
	- note that *Common Lisp* allows for dynamic *and* static type checking
## Unchecked
- C's `void *`
- Odin's `rawptr`



# Appendix - See Also

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
