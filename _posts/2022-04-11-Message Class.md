---
layout: post
title:  "Message Class"
---

I'm experimenting with a `Message` class that has two main fields and two trace fields:
1. tag
2. data
3. come-from id
4. previous message.

Since each message is defined as above, `previous message` becomes a nested list from the beginning of time.

Currently, I output traces in Lisp syntax and use a Lisp pretty printer to view them (emacs *indent-region* in my case).

Fields (1) and (2) are *real*.  Fields (3) and (4) are for debugging[^deb].

[^deb]: See "Tracer Bullets" for description about what (3) and (4) are.

## Tag In Practice

I found that, in practice, I wanted to tag messages - always.  

One untagged input (like Unix stdin) was not good enough in practice.

I wanted to know *why* a message was being received.

A *tag* is a simple code - a number, a symbol.

I tried using untagged messages, but, then when I put tags back in, I had to hack on the kernel.

This made me think that tags are *atoms* and need to be explicitly taken into account in the kernel.

I dunno, maybe some day when I have copious free time, I will reconsider the pervasity of tags and normalize them out of the kernel.

## Messages In General

Tagless messages have an appeal.  

Messages should be layered envelopes like network packets.

Each Layer in the code picks off one layer of wrapping and passes the data on.

### OSI Layer Model

The OSI 7-layer model in-the-small, applied to software components.

Will it turn out to be 7 layers for component-driven software?  

I don't know yet.  

My current guess is that it won't turn out to be hard-wired to any specific number and will depend on the problem-being-solved.

Maybe a cookbook of layer-patterns can be created for programmers who don't want to invent new layer patterns.

## Tag Handlers

A tag handler is a pure λ that takes two (2) parameters
- me (self, this)
- message.

The uber-controller contains one λ for each possible message tag.

The uber-controller decodes tags, then, calls the appropriate λ to handle the message.

Tag handler λs can call `Send()` to send messages upwards for routing, but, handlers cannot invoke other handlers directly.  

Only the parent Container can route messages.  This provides *flexibility* and allows components to be used in differing situations.  

## Libary Functions Are Inflexible

We *thought* that library functions work this way, but they aren't flexible enough.  

For example, any library function that invokes another function by-name (which is the usual case), is inflexible and has the name of the other function baked into it.

DLLs are a partial solution to this problem of flexibility.

DLLs wouldn't be necessary if software components were flexible-by-default.

## See Also

[Tracer Bullets](https://guitarvydas.github.io/2022/04/11/Tracer-Bullets.html)

[Table of Contents as of Dec. 01 2021](https://guitarvydas.github.io/2021/12/10/Table-of-Contents-Dec-01-2021.html)
[Blog](https://guitarvydas.github.io)
[Videos](https://www.youtube.com/channel/UC9EJr0nKHwadbHUtc5zHdmQ/videos)
[References](https://guitarvydas.github.io/2021/01/14/References.html)
[Books](https://leanpub.com/u/paul-tarvydas.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 