## Visual Programming
It is currently believed that Visual Programming is a failure.

This is true when VPLs are designed using the religious filter of treating all operations in a step-wise manner.

Drawing diagrams of step-wise programs is make-work.  Textual notation is more concise, and, more familiar to even school children, for expressing this kind of thing.

Yet, diagrams of computer networks make sense to every programmer.  Those kinds of diagrams *do* work.

Yet, when CEOs draw sketches on whiteboards, their minions tend to understand what needs to be implemented.

Can we restrict visual syntax to be more rigorous?  Invent rules for drawing programs?  

We did that with English prose.  We chose only a few words, like `if...then...else` and threw away most of the other words in the English language.  Then we built recognizers for the restricted syntax - the chosen words.

VPL design is not about recognizing all of Art, but, of culling the most useful tidbits from diagrams and using them to build programs for sequencing pEMs (aka "computers").

And, then, we need to break the religious belief in synchronousity.  The programs that we want to draw with diagrams are truly asynchronous, not just step-wise-simultaneous.

## How?

We have lots of tools for parsing text.  My current favourite is Ohm-JS.  I favour any PEG-based technology over any CFG-based technology.

We want to parse diagrams, though.  Note that we don't want to convert text into diagrams, we want to grok diagrams and compile diagrams into executable code.

Many current diagram editors convert diagrams to text in a format called XML (mxGraph, etc.). 

Can we use parsers to grok XML diagrams?  

Yes.  

See below (Example, Inspiration).

I currently favour `draw.io` and `excalidraw` for diagram editing.  These editors are not fine-tuned for drawing programs, but, you have to start somewhere.
## GPT
If GPT can parse English language, maybe it can grok diagrams?  This remains to be explored.

What if we use pencil and paper to draw diagrams, then, took a picture of the diagrams with our smartphones, then uploaded the pictures to GPT for parsing and compiling to code?
## Example, Inspiration

We've been using `draw.io` to draw diagrams of programs and to compile them to Odin (a better "C") and to run them.

The latest variant of this stuff is in https://github.com/guitarvydas/transpiler .  Branch `dev`.

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
