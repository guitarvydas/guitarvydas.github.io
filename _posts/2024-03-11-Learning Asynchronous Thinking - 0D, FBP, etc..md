[This note is intended as a specific answer regarding FBP ...]
# How Do I Get a High-Level Overview of FBP?

# How Can I Learn This Paradigm, Today?

UNIX pipelines are maybe the closest concept to FBP. Closures, daemons, clients, servers, networking are all similar to FBP. Maybe Go is in the ballpark (I don't use Go, but Rob Pike was involved in its design). If you know how to use those concepts, notice how easy it becomes to plug components together, and, notice that you don't need to follow a strict 1-in:1-out policy, like with function-based thinking.
# FBP-ish Tools Built Using Synchronous Languages

- Flyde
- noFlo
- Nevalang (I don't know enough about Nevalang yet)
- etc.

# True Asynchronous

At present, we only fake out true asynchronicity, but, some notations avoid the function-based paradigm and are ready to be used in truly asynchronous (aka "distributed") systems:

- 0D
- FBP
- networking protocols
- UNIX-style pipelines using multiple FDs (not just stdin, stdout, stderr)

True asynchronous notations are characterized by:
- no memory sharing
- multiple inputs and multiple outputs. 

"0D" is my take on this problem. 0D should be familiar to FBPers, but is subtly different. To discuss 0D, please join the discord server https://discord.gg/ZaFekNRP. (Everyone welcome).
# Longer Answer
FBP is asynchronous processing brought down to a programming language level, making it more convenient, more flexible and more efficient than many other approaches. 

The best that languages like Python, Rust, Haskell, C++, Smalltalk, etc. can do is to *react* to asynchronous events in an internally-synchronous manner. 

Function-based thinking is *not* asynchronous and can never be truly asynchronous. True asynchronicity is "free will". Function-based step-wise simultaneity is not asynchronous because all components are expected to operate in lock-step, i.e. without "free will".

Most implementations of FBP, and Actors, etc. fake out asynchrony on a single computer using step-wise simultaneity and threads. 

FBP is a notation for true asynchrony instead of step-wise simultaneity. 

You can build a truly asynchronous system by using 100's of bare Arduinos and rPis - no need for Linux - and having them talk to each other across wires, i.e. absolutely no shared memory. 

The internet is truly asynchronous. We have "problems" dealing with the internet because we try to impose synchronous-style thinking on top of a phenomenon that is truly asynchronous. To do this, we need to spend time and efficiency inventing work-arounds to get over the impedance mismatch between synchronous programming languages and true asynchrony. 

Note that electronics ICs are truly asynchronous, i.e. using asynchrony to create solutions to problems is entirely possible and not all that difficult, but, it does require a fundamental change in approach and thinking. Note that in a factory containing lines of conveyor belts, the workstations are truly asynchronous - when one station fails, the other stations remain working (although they might not produce anything useful, if the failing station is on their critical path). Implicit - hidden - coupling between software components makes it difficult for us to deal with truly asynchronous systems, like the internet (blockchain, robotics, etc.). FBP is one alternative for dealing with such systems. There are other ways to deal with these kinds of problems, but, more function-based thinking ain't one of the reasonable ways. 

In a truly asynchronous system, you *cannot* care how nodes are implemented. Nodes might be composed of pure functions, or, nodes may contain *state*. You cannot know, nor do you care. Imagine hitting a specific server from your Firefox client. Is the server written in a pure functional manner in Haskell, or, is it written in Perl, or, is it just a bunch of CGI scripts written with Bash? You don't know and you don't care. 
# Basic Models
FBP uses the conveyor-belt factory model. Every node is asynchronous, starting at the bottom, and nodes communicate by sending streams of data to one another.

0D uses the electronic circuits model. Every node is asynchronous starting at the bottom and nodes communicate by sending messages and blips to one another.

In message-passing, every node is asynchronous starting at the bottom and nodes communicate by sending message to one another. Message-passing got a bad name because it was originally used in an unstructured manner - kinda like using GOTO at the assembler level instead of GOTO-less programming prescribed by more modern languages.

Note that Smalltalk does not use "message passing". Smalltalk uses synchronous method calls that were mis-named "message passing".

The async model used in function-based programming is a work-around that force-fits asynchronous processing onto the function-based paradigm. Function-based programming started in FORTRAN, Lisp 1.5 and ALGOL. Function-based programming uses the simplifying assumption that subroutines are equivalent to functions. It seems that, later, it was forgotten that this is only a simplifying assumption. Force-fitting concepts into a paradigm that fundamentally rejects the concepts results in bloatware.

Most of the concept of streaming can be expressed in a function-based manner, but, avoids the central issue - decoupling. Internet servers and internet clients are, by definition, decoupled. A stream of data sent from an internet server to an internet client is, therefore, decoupled, whereas two functions on the same computer are not decoupled, i.e. functions can call other functions, causing blocking and other coupled, synchronous behaviour. Sending streams of data between such functions does not change the coupling behaviour, but only masks it further.
# Structured Composition
All models need to be "structured" in some way to allow scaling and abstraction.
# Visualizing Systems
Drawings make sense only if the nodes on the drawing are fully decoupled and distinct from one another. 

Choosing to use truly asynchronous notations, allows one to make drawings of architectures. We see this phenomenon, in its infancy, in drawings of computer networks. Can we do better, can we be more precise?

- drawware
- drawFBP

Most attempts at drawings that use function-based thinking fail or encounter severe difficulties because of over-coupling. Hidden coupling exacerbates the problems. This has affected the way most programmers think of drawings. Programmers tend to believe that drawings are useless and overly-complicated. This belief is based on bad experiences with synchronous, function-based implementations of drawings. Yet, we see other professions using drawings as their main means of Engineering, e.g. engineering of buildings, engineering of bridges, schematics in electronics design, drawings of molecules, etc., etc.
# Summary
FBP is one way to deal with asynchronous systems, like the internet. 

To learn about the FBP paradigm, the best thing you can do right now is to study fake-outs of asynchronous systems, like UNIX pipelines, internet servers, EE, etc. Studying synchronous implementations of Actors, processes, and workarounds like function-based async paradigms, cannot easily give you an appreciation for the benefits of asynchronous thinking.   

UNIX pipelines are close to being structured because of UNIX's use of hierarchical file systems. UNIX shell scripts can invoke other shell scripts. You can write structured systems in this way, but, you have to be careful not to abuse the paradigm by using shared memory or rats' nests of interconnections. Text-only syntax, unfortunately, encourages flatness in architectural designs.

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
