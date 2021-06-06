---
layout: post
title:  "Connecting Layers"
---

What is the minimum unit of connect-ability?

Imagine that we want to connect one software module to another.

What do we need to know to do this?

# Connecting Audio Signals

Let's imagine a physical real-world system.

Imagine that we want to connect a guitar to a guitar amplifier.

We connect the two using a cable ("guitar cord").

The only "typing" applied to the cable is the physical connector and the receptacle that it is going to be plugged into (e.g. 1/4-inch plug to 1/4-inch jack).

Is the signal analog or digital? Is it +5V or +3V?

The cable doesn't care.

# Connecting Software Modules Together

What is a software cable?

Can we connect two software components via a chain (pipeline) of increasingly specific type filters? Bits in at one end, type "xyz" out the other end?

Or, do we connect the software components using a smart cable?

How many smart cables do we need?

Let's imagine a very simple example. A box that generates "Hello World" strings.

Can we connect that box to a calculator box?

Maybe we have a "string-to-string" cable and a "number-to-number" cable? And a "string-to-number" cable? Do we need a "number-to-string" cable?

How many smart cables do we need?

# Networks

Networks send packets of information.

Information is wrapped in layers of information.

Can my computer send a request to that server? 

Yes. 

I only need to know the port number. 

I can send any kind of information to that server on my port-number-cable. 

The server has a "line filter" that rejects my information if it doesn't look like a valid HTTP request.

That "line filter" is a type checker.  More generally, it is a design-rules checker.

That line filter strips off the outer-most layer of information and passes the rest on down the line.

After my data passes through the first line filter, my data is passed through more checkers. 

How many more filters are there?

I don't know. 

I only know what I need to know.

If I wrap my data in the correct set of layers, it will make it all the way to the end and I will receive a response (wrapped in layers that I define or agree to).

Today's software cables are based on the all-in-one mentality instead of the layered mentality.

We are - slowly - beginning to rediscover what networking people already know, what electronics people knew before them, etc.

# Layered Data

We need to wrap information like Russian Dolls.

Wrapping data in layers will allow us to build checkers that can be bolted into pipelines.

# No Dependencies

Software layers cannot poke information through to other layers.

We learned that lesson with so-called global variables, and, with Structured Programming. 

# Scoping

Scope everything.

Currently, Types and Functions are not very well scoped.

# Trees

Trees are hierarchical and do not poke information (incl. control flow) through to other layers.

## Graphs

Graphs allow cross-talk between nodes.

Graphs are not truly hierarchical.
## DAGs
DAGs allow cross-talk between nodes.

DAGs are not truly hierarchical.

## Optimization
Optimization sometime requires poking information through layer walls.

This can be necessary, but, should be delayed as long as possible, since, by definition, it destroys (poke holes into) otherwise pluggable designs.

## Low-Level Operations

Any PL[^pl] that provides, say "+" or "cons", is too low-level for structured design and harms plug-ability of modules.

# Transport Layer for Functions

Referring to OSI's model of layered networking, what is the Transport layer for functions?

Do libraries obey the OSI model at the function level?

# CPU

Most CPUs define the unit of pluggability to be the _byte_.

Assembly op-codes are built on the assumption that instruction sequences have been pre-filtered.

Additionally, many CPUs also define _sequentiality_ as a unit operation. Opcodes are sequential[^seq].

[^pl]: PL means Programming Language

[^seq]: There is no inherent reason that opcodes are interpreted in a sequential manner. In fact, the internal electronics of CPUs has circuitry to impose a sequential regimen onto opcode processing (i.e. this is a Design Choice, not inherent in the electronics itself). 
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
