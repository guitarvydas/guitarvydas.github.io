The Holy Grail of mathematics is to convert all understanding into some normal form.  This form is usually text-based.

The idea is to convert *all* information into text, then to manipulate the text using repetitive applications of "Laws" and "Theorems".

Data structures are laid out in text, but, the data contained therein is not represented as text.  The data is usually represented as something hung onto the data structures. 

## Syntax-Directed Translation

Imagine a system with no data structures, just text.

Instead of sticking information into some hoary data structure, you just annotate the text with textual information.  Then use text parsers to extract and grok the information.

We didn't use to do this in the past, only because it felt "inefficient".  Data structures store data in a more concise manner.

Now, the ground rules have changed.  We can be wildly inefficient compared to the past.  Heck, we even use JSON.

So, what does a text-only programming system look like?  Uh, mathematics?  How do you grok this kind of stuff?  Uh, parsers (esp. PEG, esp. Ohm-JS).  How do you read this stuff?  Uh, you don't, only the machine needs to read it.  How does this help?  Uh, programmers can build programs in little pieces and pipeline them together on a conveyor belt.  The input text is ingested by a series of barnacle processors.  Each barnacle adds its own information to the text then passes it down the line to the next barnacle.  In fact, some barnacles may wish to subtract information to make for less work downstream.

Have we seen this before?  Yes. UNIX® shell pipelines.  The problem with UNIX® is that it over-specifies the format of the text - it demands that things be chunked on line boundaries separated by newlines.  That format is too linear, non-recursive and too restrictive.

Have we seen better text formats before?  Yes. FBP - Flow-Based Programming - defines brackets that can be nested.

Have we seen even better text formats before?  Yes.  Textual programming languages encode information as "structured text".  PT Pascal was an early example of how to ingest this kind of stuff in a piece-wise manner and to compile it to executable form.

Are there other names for this kind of thing?  Yes. "Transpilation". "Source Transformation".


## Appendix - PT Pascal and S/SL 

https://research.cs.queensu.ca/home/cordy/pub/downloads/ssl/

## Appendix - Language Implementation by Source Transformation

https://qspace.library.queensu.ca/server/api/core/bitstreams/39e5a65a-79b8-4986-a07e-c7033bf675e5/content


## See Also
### Blogs
- https://publish.obsidian.md/programmingsimplicity (see blogs that begin with a date 202x-xx-xx-)
- https://guitarvydas.github.io/
### Videos
https://www.youtube.com/@programmingsimplicity2980
### Books
leanpub'ed (disclaimer: leanpub encourages publishing books before they are finalized)
https://leanpub.com/u/paul-tarvydas
### Discord
https://discord.gg/Jjx62ypR  ("programming simplicity") all welcome, I invite more discussion of these topics
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
