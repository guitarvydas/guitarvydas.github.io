---
layout: post
title:  "Asynchronous Software Components Design Note"
---

A stand-alone Software Component is characterized by:
- a name
- a bag of synonyms
- a namespace for inputs
- a namespace for outputs
- a namespace for for children components
- a namespace for connections.

Naming of software components is relative
- `./` refers to the current component
- `./i/N` refers to the Nth input (N is an integer)
- `./o/N` refers to the Nth output (N is an integer)
- `./c/N` refers to the Nth child (N is an integer)
- `./x/N` refers to the Nth connection (N is an integer)
- `./c/N/i/M` refers to the Nth child's Mth input
- `./c/N/o/M` refers to the Nth child's Mth output
- it is not possible to refer to a child's children nor its connections.

Note that only Container Components contain namespaces for children and connections.
# Container Component
A _container_ component contains 1 or more children components.

_Container_ components a composed of other components.

_Container_ components all behave the same way
- `handler (e)`
 The input handler distributes incoming messages by distributing them using the connection namespace.

peration).

 Input messages are normally distributed to children.

 Input messages can also be sent directly to a _container_ _asc_'s output.
 
 - `initialize ()`

 There is no user-supplied initialization for a _container_ _asc_. 

 From the users's perspective, _initialize ()_ can be called, but is a noop (no operation)
 
 A _Container_ _asc_ is composed of other _asc_s. 
 
 A _Container_ _asc_ can contain _container_ _asc_s and _link_ _asc_s.

 It is not possible to know the implementation of contained children _asc_s. 

# Link _Asc_

A _link_ _asc_ contains 0 chilren and 0 connections.

A _link_ _asc_ has only a `name`, `inputs` and `ouputs`.

# Connection
A connection consists of
- a name (mostly for debugging)
- a sender
- a receiver.
## Sender
A Sender is a reference to a child (or self) along with a tag
## Receiver
A Receiver is a reference to a child (or self) along with a tag
## Multiple Receivers
A Send () can distribute an message to multiple receivers.

The system guarantees that all receivers attached to the same output, receive the same message in an atomic fashion. 

N.B. Atomicity is "automatic" when all _asc_s reside in the same thread.

N.B.
# Bare Metal and Multi-Threaded
Note that the following applies only to implementations that employ multiple operating system threads or are on bare metal (no operating system at all).

When the system is implemented with all _asc_s residing in the same thread in an operating system, "locking" is automatic (a by-product of sequential operation) and the considerations listed below can be ignored.

To deliver an message to all receivers from one output, the Dispatcher:
1. locks all receivers related to the output
2. appends the message to the input queue of all receivers, N.B. the message tag is rewritten from being an output tag of the originating sender to the input tag of the receiver.
3. unocks all receivers related to the output

# Message
An message is characterized by two details:
- a tag
- data.

A tag is a string or a symbol that is used to qualify the intended destination of the message.

Data can be _anything_.

Data is usually some kind of data entity that is supported by the base language. 
# Message Delivery Layer
## Type Checking
### Layered Type Checking
Type checking in this system is not an _all-in-one_ process.

Types are checked in layers.

Analogy: OSI 7-layer model.

Analogy: Russian Dolls.

Analogy: Layers of onion skins.

As far as the ASC system is concerned, there is only one - very simple - type: the Message.

This ASC system delivers Messages and does not concern itself with the actual contents of the messages. Further checking is the responsibility of higher-level _asc_s.
# Standard Methods
## Handler
Every __asc__ handles incoming messages (see the definition of a tagged message).

Every __asc__ has a `handle (e)` method that takes one parameter - a tagged message.

## Initialize
Every __asc__ has an `initialize ()` method that takes no parameters.

The `initialize ()` method is called before any calls to _handle (e)_.

The `initialize ()` method is called after a __asc__ has been instantiated.

## Instantiation
__Asc_s_ are instantiated in a manner similar to objects in OOP.

_Container _Asc_s_ instantiate their children recursively, during instantiation.

The instantiator returns the instantiated _asc_ so that the instance may be used in creating containing _asc_s. This is a recursive process, so that _container _asc_s_ can contain other _container_ _asc_s).
# Templates & Runnable Instances
A __asc__ is defined by its _template_.

_Templates_ are like _classes_ in OOP systems or _prototypes_ in JavaScript.

A __asc__ can run only if its template has been instantiated into a _runnable instance_.

A _Template_ can be used to produce one or more _runnable instances_.

[N.B. This is very similar to instance and classes in OOP systems.  _Templates_ and _runnable instances_ might be considered to be derived from OOP.  ASCs emphasize concurrency and isolation.  ASC _templates_ are not general classes like OOP classes.]

Roughly, a _template_ defines an ASC, its inputs and outputs and its children and connections between children.

Connections are internal to the _template_. 

Connections can only connect children _ascs_ together (and the self container).

Connections are not exported from the _template_.

A _runnable instance_ created from a _template_ has a unique set of child instances and a unique set of connections between those children. 

The _shape_ of the connections are specified by the _template_, but the actual connections are between unique instances of children (and self).  In other words: each instance of a _template_ has the same kinds of connections as specified by the _template_, but the actual end-points of each connection are unique to the instance.

Roughly, a _runnable instance_ creates a unique instance of an _asc_ from a template, and, creates a unique input queue and a unique output queue for each instance.

Each _runnable_ instance has exactly one input queue and exactly one output queue for messages. 

Message tags provide finer granularity for each message.
## Templates
(see discussion above)
## Runnable Instances
(see discussion above)
# Isolation
Messages are routed by the direct parent _container_ of the _asc_, not by the _asc_ itself.  

_Ascs_ are isolated. 

_Ascs_ cannot refer to other _ascs_.

_Ascs_ can only send messages "upwards" to their _containers_ (direct parents) for routing.

Only the _container_ "knows" where a message originates and where it is sent to.
# No Connection
Outputs of an _asc_ can be directed, via the connection table (a routing table), to other _ascs_.

Connections can be directed at 0 (zero) or more other _ascs_.

Connections that go to 0 (zero) other _ascs_ are termed N/C (No Connection).

A missing connection is treated as an N/C.

Messages sent to N/C are discarded.

Inputs can, also, be N/C. 

An N/C input never fires (IOW: never invokes the _asc_ with the input's tag).

# Inputs and Tags
An _asc_ appears to have multiple inputs.

In reality, an _asc_ has exactly one input queue.

All incoming messages are placed onto that single queue.

Each message is _tagged_ with an identifier defining "which input" the message came in on.

Analogy: A Web server uses one computer, but has multiple ports. Ports are differentiated by intege tags called "port numbers".

# Standard Output Methods
## Send
_Ascs_ communicate by using the `Send ()` method to send messages.

Messages are routed by the direct parent _container_ of the _asc_, not by the _asc_ itself.  
### Parameters
_Ascs_ do not have traditional parameter lists, and receive inputs as tagged messages.
### Return
_Ascs_ do not have traditional return values, and send values using the `Send ()` method.
### Exceptions
_Ascs_ do not have traditional exception handlers, but send values using the `Send ()` method.
# Happy Path vs. Other Valid Outcomes
One point in the design of _ascs_ is that _ascs_ can have more than one valid outcome.

The distinction between the _Happy Path_ and other valid outcomes is blurred.

In some ways, _ascs_ treat all outcomes "first class citizens".

Exceptions are not exceptional. Exceptions are, but, one valid outcome.
# Message Fan-out and Copying
# Queues
There is exactly one input queue for each _runnable_.

There is exactly one output queue for each _runnable_.
# Deferred Sending
When an _asc_ sends a message, the message is not delivered immediately, but is placed on the _asc's_ output queue.

The output queue of an _asc_ is emptied (distributed) only when[^deferred] the _asc_ has finished processing one input event.

[^deferred]: Actually, output queues are emptied _some time_ after the _asc_ has finished processing.  The actual implementation of delivery is implementation-dependent.  Concurrency is the rule, not the exception, and __asc_s_ cannot run if they are, recursively, busy (I believe that all details emerge from this set of rules).

The _Dispatcher_ distributes output messages from the output queue of an _asc_ to the input queue(s) of other _ascs_.

Messages are delivered using the connection list of the _container_.  A particular _asc_ cannot know where its output messages are going (nor where its input messages originated).

[Edge-case: messages can, also, be delivered to the output queue of a container.  This is essentially an internal `Send ()` employed by the container handler routine. (All _containers_ share the same `handler ()` routine).]

# Dispatcher
The _Dispatcher_ is a distinguished routine that runs the system.

The _Dispatcher_ invokes __asc_s_ and expects them to process one event to completion. 

(See the section regarding long-running loops and deep concurrency).

Essentially, the _Dispatcher_ maintains a list of every _asc_ in the system and invokes _asc_ - in any order - that are ready-to-run.

[Aside: Since _containers_ cannot run if any of their children are busy (recursively), it might be possible to have the _Dispatcher_ maintain only a tree of _ascs_ instead of maintaining a list of all existing _ascs_. Each _container_ maintains a list of its children ; maybe the _Dispatcher_ need to keep only a list of top-level _containers_. This optimization is left as an open consideration and is implementation-specific.]
# Asynchronous Operation, Concurrency
All _ascs_ are asynchronous and concurrent.

[Aside: this means that _ascs_ cannot be implemented simply as callable functions.  Such functions imply synchronous operation.  This is a subtle point.]

# Run Forever
_Ascs_ run forever.

There is, also, a start-up time, and, a shut-down time. _Ascs_ run forever in the _steady state_ time (the majority of an application's lifetime).
## Like a Event Loop
It might be useful to imagine _ascs_ as being GUI components that run in event loops.
# Long Running Loops / Deep Recursion
_Ascs_ must not[^promise] run for a "long time" and/or execute "deep recursion".

[^promise]: 
## Cooperative 
_Ascs_ run cooperatively. 

This removes a major source of accidental complexity - full preemption.

This adds the onus on the programmer to ensure that an _asc_ runs to completion in a "small" amount of time.

Note that, it is possible to have compilers emit _loops_ that are not loops but self-message-sends, which would alleviate the major, non-bug, reason for long-running loops.

Currently, we use hardware (MMUs and interrupts) and Operating Systems to ensure full preemption.  These techniques could be used to ensure against long-running loops.

The use of Operating Systems and the reliance on long-running loops has caused subtle accidental complexity, e.g. priorities, which lead to priority inversion.

I urge programmers to stop using Operating Systems altogether.  I urge programmers to design software that is directly suited to the problems-at-hand instead of relying on one-size-fits-all technologies like Operating Systems and the current crop of 3GL, loopful[^loop] languages (e.g. Python, Javascript, Haskell, Rust, etc..

[^loop]Loops are a subset of Recursion. I urge programmers to avoid recursion. Recursion does not suit the new reality - distributed programming. Loopful languages encourage programmers to solve distributed programming problems using low-level, assembler-like operations such as thread libraries. Loops, an Recursion, should only be used to program single nodes in distributed systems. Programmers should write programs that are inherently distributed and push minor details, like implementation of nodes using looping/recursion, aside.
# Resolving
## Incremental "Linking"
UNIX ar.
# IDE
 Only the IDE can know how _asc_s are implemented.
 
 The IDE checks that all _asc_s are _resolved_ before executing an application constructed using components.
# Composition
Not inheritance.
# Execution
# Example
## Sample Diagram
## Sample Implementation
## Common Lisp
## JavaScript
## Python
## WASM

# See Also

spaghetti
[References](https://guitarvydas.github.io/2021/01/14/References.html)
[Table of Contents](https://guitarvydas.github.io/2021/05/14/Table-Of-Contents.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
