---
layout: post
title:  "The Atomic API"
---

The most _atomic_ API consists of a function with exactly one parameter and zero return value(s).

```
function api(param) {...}
```

The function runs forever.

The function parameter is always of type `event`.

An `event` message contains two fields
- a tag
- data.

# Type Checking the API
Type checking consists of ensuring that the `event` parameter is the correct shape (as above).

# Layered Type Checking
Further type-checking is a layered form of the `event` data, like newtork packets.

We can string type-checking filters together to successively ensure that events arriving at a software component are "valid".

This is akin to input validation for web-based forms (i.e. we already do this kind of type checking).

We call this kind of type checking by a pipeline of filters _design rule checking_. 

Type checking by pipeline has had  several different names, e.g. input validation, business rules, OSI 7-layer model, etc.

There can be no general definition of data within `events`. 

The definition of data is agreed upon by the sender and the receiver (much like the meaning of text lines in UNIX pipelines).

An `event` tag is sufficiently large to hold a small `int` (0-31), i.e. the tag is on byte in size.

The `data` portion of an event is at least 3 bytes long.

The minimal `event` data structure is
- 1 byte tag
- 3 bytes data.

Larger events are accomodated by agreement of the sender and receiver.

Typically, the event `data` field contains layered information. The layers are peeled by a pipeline of receivers.

Events larger than 4 bytes are 
1. parsed by a pipeline of receivers, or, 
2. treated as garbage by the receivers (note that large events can appear as successive garbled messages). The Software Implementor(s) must ensure that components are correctly connected together. It is advisable that software components be designed with a _reset_ input that drives the component into a known, default state.  Systems can employ `watchdog timers` that reset components much like watchdog timers in hardware designs.

It is advisable to design components in a manner similar to the OSI 7-layer model for networking. (Aside: components can contain component pipelines themselves, in order to process events in a layered manner).



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
