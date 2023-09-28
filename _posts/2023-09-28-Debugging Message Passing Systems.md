
A message passing system is composed of a bunch of computing nodes that communicate with each other solely by passing Messages to one another.

To debug such a system, you want to track the provenance of each message through the system of nodes.  

Tracking the *control flow* through one node is but a secondary aspect of debugging a message-passing system.

## Debug Mode
- keep every message (do not free messages, do not garbage collect messages)
- tag every message with a pair : { component, causing message }
- tag every component with its owner (like *parent*, but, a dynamic chain of instantiations)
- if the program is "small", or of "short duration", then we can keep all messages and destroy them in a Biblical Flood method (i.e. the kind of garbage collection used by UNIX® when finalizing processes)

- debugger can examine provenance chain for any messages
	- who sent the message
	- what incoming message caused the handler to fire
	- when a particular node has been isolated, existing *control flow* debuggers can be used to examine the flow within the node

## Production Mode
- long-running code
- keeping all messages leads to "memory leaks", i.e. depletion of memory
- discard messages - free messages, garbage collect messages

## Debuggable Production Mode
- allocate messages in generations
- garbage collect generations when they become "old", 
	- e.g. after a few hours
	- e.g. after a day
	- e.g. when memory becomes scarce
	- etc.
- do we need to fixup every reference to every freed message? or,
	- can we invalidate the space in which freed messages used to reside? (e.g. mark a block of addresses as unavailable)
	- use virtual memory methods to page debugging information out to cheaper, more abundant storage
- or, fine-tune message provenance checking to keep as little useful information as possible
	- what information to keep? 
		- depends on the application
		- cannot be fully generalized
		- might be classified in terms of kinds of information that can be efficiently kept


## See Also
### Blogs
https://publish.obsidian.md/programmingsimplicity (see blogs that begin with a date 202x-xx-xx-)

https://guitarvydas.github.io/
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
