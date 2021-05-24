---
layout: post
title:  "The Trouble With UNIX"
---

# Early BASIC

In the early days, BASIC was based on bytecodes, called _VM_s today.

The trouble with this approach was that other people could read and modify the application code without clearing the changes with the owners.

At the time, this was considered a business problem, but it goes much deeper than that.

It was thought that, since anyone could read the code, anyone could copy the code and undercut the business by offering the same software product without expending the same amount of sweat equity.

Today, the problem manifests itself differently.  Open-source has taken away the profit motive, but,
1. a hacked[^hack] application might not operate as documented (hurting the Brand), and,
2. a hacked application might perform nasty operations that weren't part of the original program.

[^hack]: Hack and hacker used to be badges of honour.  Today they are more likely to indicate criminal behaviour.

# The Trouble With UNIX /bin/*sh

The UNIX shell, all flavours of /bin/*sh, has the same problem as early BASICs.

I don't like building apps that have "too many" moving parts and rely on files and operations that can be tweaked, hacked, by the user.  In the best case, such applications might fail in the field and cause maintenance headaches for me.

OTOH, I like building apps using pipelines of isolated components.  /bin/*sh is good at this.

I need a way to ship applications built as shell scripts, that won't fail in the field.

I need a "coordination language".  I need a PL for distributed programming, that produces apps in the way I might produce apps in any current PL (e.g. Python, HTML+JS, etc.), but lets me build the apps using the comfort of pipelines.

# Docker

Docker is the proverbial Canary in the Coal Mine.

Other people have already realized that they need to build self-contained apps that don't fail in the field.

## Problems With Docker

Docker fakes out a whole operating system.  This is a heavy weight solution to a more general problem.

Docker assumes that I want to build apps using one of its supported O/Ss.

Docker doesn't run well (if at all) on smart phones.

Q: What are the reasons why Docker isn't used for _every_ app?

Q: What are the reasons why _every_ function is not put in its own Docker envelope?

# Stripped Down Docker

I want[^think] a stripped down Docker-like IDE+PL.

[^think]:I think that I want a stripped down Docker.  I would be happy to be convinced that I'm wrong.

# Diagrams - Rects, Ellipses, Lines, Text

I want an IDE+PL that supports higher level programming.  

I want to draw diagrams of parts of my apps.

I want to write parts of my apps in text[^text].

How many 1,000's of Docker components can I use before my computer begins to slow down?

[^text]: It is silly to use the power of diagrams to duplicate the kind of programming that text is already good at (e.g. numeric equations, sequential programming).  Diagrams should only be used for the kinds of things that text is not very good at, e.g. expressing networks of components, concurrent coordination of synchronous sub-programs, etc.

# Heavy-Weight?

Is Docker big and heavy?  

Or do we just need to wait for bigger and better hardware?

We don't bother to write in assembler anymore, while, at first, it seemed that compilers and HLLs were just passing, very inefficient, fads.

Should all apps be Docker'ed?  

How many 1,000's of Docker components can I use before my computer begins to slow down?

I used to build distributed credit card terminal apps that used as little as 12K (K not M) of RAM on 8-bit machines.

A typical app needed some 300 components.

Components were slightly more expensive than functions, but a lot less expensive than threads and complete operating systems.

What is the status of Docker today?  What is the trend?  What is the footprint?

## Existing PLs

Shall we forget about existing PLs, like Python, JS, etc.?

Exising PLs are, IMO, already at the end of their lifetimes.

We need to write apps using concurrent components, and, existing PLs don't support this kind of thing.

Existing PLs support concurrency by using libraries based on OS threads.  This, IMO, is like assembler programming for concurrency.  

Assembler was tamed by 
1. structuring control-flow
2. structuring data (aka scoping).

Docker appears to structure data (isolating environment variables, etc.).

Docker appears to leave control-flow unstructured and flat[^mp].

[^mp]: A sure way to shoot yourself in the foot is to create a spaghetti-based message-passing system.  Message-passing needs to be structured using hierarchy, composition, isolation, etc.  I don't know of any PL that helps you do this kind of structuring. You are left to fend for yourself using assembler primitives such as threads and rendezvous.

# See Also

[References](https://guitarvydas.github.io/2021/01/14/References.html)
[Table of Contents](https://guitarvydas.github.io/2021/05/14/Table-Of-Contents.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
