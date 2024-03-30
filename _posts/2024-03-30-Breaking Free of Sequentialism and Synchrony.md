Somewhere back in the mists of time, the concept of "synchronous" programming languages was invented and adopted.

For example, if you write code that puts one statement after another, like
```
x = 5;
y = 6;
```
it is guaranteed that these statements are executed in sequence, one after the other. In the example above, the variable `y` is mutated only after the variable `x` has been mutated.

This idiom was invented as a simplifying assumption[^sp], but, has become widely accepted as the basic meaning of "programming languages".

[^sp]: Simplifying assumption: Ignoring certain aspects of a phenomenon because their effects are swamped out by the effects of other aspects, but, not forgetting about the fact that the other aspects remain there. The ability to ignore certain aspects of a phenomenon allows deep thinking about a *slice* of the phenomenon. Early Scientists, like Maxwell and Feynman, understood this concept and did not wish to form religious beliefs about over-application of certain simplifying principles. For example, Maxwell's Equations do not explain the phenomenon of electricity, they only explain a *slice* of the phenomenon of electricity. Feyman devised Feynman diagrams to think about and to explain a *slice* of Physics. Such *slices* are often useful, but, are incomplete by definition. Most real phenomena require analysis using many such simplifying assumptions. According to Nobel Laureate Ilya Prigogene, the over-use of the simplifying assumption of functional notation retarded advancement in Physics by 100 years. I assert that we've been using a simplifying assumption of function-based notation for programming, but, that we're hitting the asymptote on what that simplifying assumption is capable of, which means that we need to add more notations to our tool-bags for programming. Anything that "seems difficult", like concurrency, screams out for the use of a different notation for that *slice* of programming.

Most programming languages work this way, for example Python, Rust, WASM, etc.

A few programming languages, e.g. Prolog, break with this paradigm. Prolog seems strange and "declarative" to most modern programmers.

Note that, in the above code, the issue is not that `x` and `y` are mutated, but, that the statements happen in a very strict sequence, one after another.

This deep-rooted belief in the over-use of sequentialism and synchrony is coming back to bite us when it comes to dealing with the asynchronous concepts like the internet, blockchain, robotics, GUIs, etc.

Most things in life are not deeply synchronized in this way. Electronics ICs are not automagically synchronized by default. Human-to-human interactions are not synchronized by default.

In modern programming, we try to force asynchrony - threads - onto programming languages that defy asynchrony at their core. We build asynchrony on top of synchronous languages which have been designed to remove asynchrony. Dealing with asynchrony using synchronous languages is make-work.

Even the concept of *functions* causes heartburn, by sprinkling ad-hoc blocking throughout our code. The band-aid fix for this problem is the concept of *preemption*, employed by all modern operating systems. *Preemption* comes with a lot of baggage and *gotchas*. For example, the Mars Pathfinder fiasco caused the invention of another band-aid glued on top of the band-aid of *preemption*. This epicyclic band-aid is called "priority inheritance".

CPUs are simple ICs. CPUs - by *definition* - work in a sequential, synchronous, single-threaded manner. This does not mean, though, that our high-level languages *need* to work in this manner, too. Yet, most HLLs are designed to be sequential and synchronous by default. This meme is very prevalent and affects - at a very deep, intuitive manner - the way that modern programmers think.

Most programmers equate the concept of sequential synchrony with the concept of "programming language". This doesn't need to be the case, but, it is the case.

# Protocols
One way to break free of the sequential meme is to invent protocols which insert sequentialism and synchrony into a design only where needed.

Networking does this.

Humans do this, too. They don't even notice that they're doing it. For example we have protocols for
- meeting people - we shake their hands
- starting a meeting on time, even when all of the participants have not arrived yet (shades of *blockchain*)
- delaying the start of a meeting until someone important arrives, like the speaker or the CEO
- traffic lights at road intersections
- pictures of circles and rectangles on white-boards joined by arrows, humans implicitly assume that the circles and rectangles are *fully decoupled* from one another
- in Zoom meetings, only one person speaks at a time, since the audio becomes muffled and distorted when too many people speak at once
- Christopher Alexander's "Pattern Language" concepts. Unspoken is the fact that each pattern is utterly stand-alone and decoupled from all other patterns. Such concepts cannot be directly implemented in synchronous programming languages without the addition of workarounds.

I argue that we need to remove default synchronization from HLL programming languages and should let Software Architects and Software Engineers insert explicit sequentialism and synchrony into a design on an as-needed basis. 

Kinda like designing network protocols at a statement level. 

Little networks.
# Ethernet is Not Synchronous
Can default asynchrony work at all and not cause confusion? 

Ethernet is a very successful protocol for wiring computers together.

Ethernet contains no sequentialism nor synchrony in its design - *at all*.

Ethernet is a good example of what can be done without sequentialism and synchrony.

Ethernet nodes do not synchronize with one another. An ethernet node simply samples its own output. If the output is *garbled*, then a collision has occurred - some other node is trying to speak at the same time. Ethernet nodes don't synchronize with one another and don't take turns at speaking, they simply "back off" for a "random" period of time and try again, when a collision has been detected. They "back off" over and over again until they get their message out ungarbled.

This seems to work pretty well and seems to be efficient-enough. In fact, it is probably a more efficient strategy over that of using synchronized "ring networks".

The design of ethernet may have given the original low-level designers gray hair, but, this design frees the rest of us from having to worry about too much sequentialism and synchrony.

Other designs for network protocols tend to be more brittle. For example, synchronizing by passing a baton around becomes confused if the baton gets broken. Yeah, you can fix that problem (by applying more synchronous, epicyclic band-aids), but, you don't have to fix it, since ethernet is "good enough".
# 0D
So, what does a non-synchronous programming language look like?

Prolog and HTML are examples of "declarative" languages that don't have synchrony built into them. There are places where you *must* have synchronization, but, the Software designers get to choose where those places are and they deal with those cases explicitly, instead of paying for over-synchronization with every line of code they write.

UNIX® shells (/bin/sh, /bin/bash, etc.) allow creating *pipelines* of isolated, stand-alone components ("commands"). The down-side of UNIX® shells is that they are text-based and they over-specify the meaning of data packets, and, they rely on *rendezvous* style concurrency. Text-based notations restrict programmers' thinking about connecting components together. UNIX processes allow for many FDs, but only a few, like s`stdin`, `stdout` and `stderr`, are convenient to use in a text-based manner. The other FDs must be handled in a clumsy way, which ultimately leads to complete avoidance of those other FDs. The use of one magic character - the newline - restricts the use of pipelines to the realm of text processing[^tp].  Rendezvous is just synchrony in sheeps' clothing. What's really needed is a visual form of pipelines[^vsh].

[^tp]: You *can* use binary data in UNIX® pipelines, but, it ain't convenient.
[^vsh]:  See VSH in the 0D examples.

My goal is to find the true *atoms* of asynchrony and to expose them explicitly to systems programmers. Systems programmers need to deal with the low-level details of synchrony vs asynchrony, but, their decisions are not peppered into every line of code that non-systems-programmers write. We should be able to make each unit of software be completely stand-alone and pluggable like LEGO® blocks. Note that current synchronous programming languages, like Python and Rust, only give the *illusion* of pluggability[^lib], but this *illusion* results in brittle software and spooky-action-at-a-distance bugs caused by unexpected dependencies between code units. 

[^lib]: code libraries

The system that I call "0D" (for "zero dependency") encompasses what I - currently - believe to be the *atoms* of software design.

One-way data sends[^one-way].

Every software unit is a stand-alone component.

Every software component has input *ports*.

Every software component has output *ports*.

Components "send" data in packets ("messages"). SENDing is deferred. SEND just enqueues outputs on a component's output queue.

Components cannot choose which other components to send data to. Routing of data messages is performed - only - by components' parents - "Containers". This lets you plug components together and to unplug and rearrange them at will. In functional programming, this feature is called "referential transparency", but, functional programming imposes a lot more *restrictions* on how routing must work.

Components come in two flavours:
1. Containers - components composed of other components, recursively
2. Leaves - components at the bottom of the tree, non-recursive, commonly called "code".

Components have exactly one (1) input queue and exactly one (1) output queue. Single queues preserve time-ordering of all messages, and, avoid, low-hanging fruit versions of deadlock, and, support abstraction - the ability to lasso and reduce a group of components into a single component with one input and one output.

Messages are 2-tuples `{port X data}`[^structure].

[^structure]: Data is *not* structured by 0D. Structuring and type-checking are applied by the programmer's design, not the 0D toolset. Basically, *data* is just a bag of bits. And, *port* is just some sort of tag (e.g. string for now) that can be queried and cased-on by the code within a component.

Components respond to every incoming message, one at a time.

Components pick apart incoming messages based on a component's *state* and on the message's *port*.

One should be able to manually implement 0D-like constructs into one's own code, currently, by judicious use of closures and queues and a single distinguished subroutine for performing round-robbin dispatching.
# Down-Sides of 0D

The down-side of 0D is that you have to *think* about adding sequentialism and synchrony into a design, rather than having it be auto-magically sprinkled into every line of code you write. 

Actually, I think of this as an up-side, but, YMMV.

Low-level designs - sometimes - need to explicitly specify ordering of messages by using synchronizer parts[^sp]. At a low-level, the program looks "more complicated", but, the result is that software units are independent and pluggable, and, only systems programmers need to deal with synchronization issues. Most often, non-systems-programmers don't need to look at such details and tend not to care that synchronization is needed deep in the bowels of some component.

[^sp]: which I currently call "1then2".

Another apparent down-side is that 0D looks a lot like the unfairly-discredited concept of "message passing". Message-passing[^mp] is like GOTO. It is a fact of life and it is fundamentally useful. To avoid blowing your own foot off, though, it behooves you to design the system in a *structured* manner which allows scalability. 

The concept of *structured message passing* becomes fairly obvious once you begin thinking this way. Components need to be arranged in a tree-like manner - like an ORG-chart in business. *Requests* flow down from a node to its children. The children respond with summarized *information* flowing back upwards. No micro-management allowed. No "going over the boss's head". This is just another example of a human-invented "protocol" that is already well-tested and in-use and successful at a large scale. For example, we see ORG-charts and avoidance of micro-management in large, scalable, successful corporations.

CALL and SEND are orthogonal concepts. Both are useful and necessary, but, our current crop of languages emphasize CALL and de-emphasize SEND.

[^one-way]: Note that bi-directional data flow is a less-efficient "molecule" built up using one-way data flow atoms. CALL and RETURN are examples of such less-efficient molecules.

[^mp]:  True message-passing between asynchronous components, not the synchronous method-calling, mis-named "message passing" found in OOP.

# Appendix - 0D
A working prototype, a sour-dough-like starter kit is in the repo [0D](https://github.com/guitarvydas/0D)

Various working examples are listed in the README.md file.

Currently, 0D uses the Odin programming language. We are close to having a Python version implemented. 

# Appendix - Illusion of Pluggability

[ALGOL Bottleneck](https://guitarvydas.github.io/2020/12/25/The-ALGOL-Bottleneck.html)

# Appendix - Message Passing

[Message Passing](https://guitarvydas.github.io/2021/03/27/Message-Passing.html)
# Appendix - See Also

### References

[https://guitarvydas.github.io/2004/01/06/References.html](https://guitarvydas.github.io/2024/01/06/References.html)

### Blog
[blog](https://guitarvydas.github.io/)

### Blog
[obsidian blogs](https://publish.obsidian.md/programmingsimplicity) (see blogs that begin with a date 202x-xx-xx-)
### Videos
[videos - programming simplicity playlist](https://www.youtube.com/@programmingsimplicity2980)
### Pamphlets
[DSL for Writing DSLs](https://tarvydas.gumroad.com/l/hiypq?_gl=1*1bdn1r0*_ga*NTI5MDkzNTI0LjE3MTAzNTQzNjU.*_ga_6LJN6D94N6*MTcxMTQ4ODE0Mi43LjAuMTcxMTQ4ODE0Mi4wLjAuMA..)

[Is Concurrency Difficult?](https://tarvydas.gumroad.com/l/dvtej?_gl=1*o7hy6z*_ga*MjA0NzUyMDY1Mi4xNzA3NDc3MDIx*_ga_6LJN6D94N6*MTcwNzQ3NzAyMC4xLjEuMTcwNzQ3NzI5Ni4wLjAuMA..)
### Discord
[Programming Simplicity](https://discord.gg/Jjx62ypR) all welcome, I invite more discussion of these topics, esp. regarding Drawware and 0D
### Twitter
@paul_tarvydas
### Books (WIP)
[leanpub](https://leanpub.com/u/paul-tarvydas)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
