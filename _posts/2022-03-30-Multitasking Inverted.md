---
layout: post
title:  "Multitasking Inverted"
---

## Elevator Pitch
I think that multitasking is backwards.

Instead of having an Operating System that call functions, we can have functions that have internal multitasking.

## Multitasking Used to be Simple

At its most basic, multitasking is a Loop with a test.

Multitasking, as a function, consists of:

- initialize "the environment"

- Loop:
	- call a function
	- store the result from the function
	- test to see if we should quit
	- repeat, from the top, if we don't need to quit

- on quit: suck various values out of the environment and return them

That happens to be the way that early games were built.  They would use up the whole CPU and all of memory for the game, and, come up for air once in a while.

That's how messaging loops work - (1) process message (2) check for quit or new messages.

### Closures, Anonymous Functions, Lambdas

Anonymous, first-class functions are all that is needed to implement concurrency (and multi-tasking).

Operating systems are just big, inefficient, implementations of anonymous functions.

## Code Bloat

We veered away from this simple model when we jammed mutation (aka Garbage Collection, etc.) into a paradigm that didn't really support all that stuff.

This resulted in bloat of the paradigm.

Instead of remaining simple, the paradigm was hacked-on.  

We played whack-a-mole with the various epicycles that were created (aka "Accidental Complexity").  

For example, the Mars Pathfinder software crashed when the Pathfinder landed on Mars.  The cause?  Ostensibly "priority inversion" in the operating system.

The *real*[^real] problem was that the operating system had grown so complicated that we couldn't see the lurking bugs until we hit an edge case - on Mars.

[^real]: By "real", I mean "the next level up".  It's turtles all the way down.  If you or I think that we've found the *final* solution, we're simply wrong.  We can always simplify the simplification and solve a new class of problems.

## Other Verboten Concepts

Once concurrency has been inverted, it is "easy" to see how to wrap other bugaboos...

These concepts aren't inherently *bad*, they simply need to be restricted in use.

For example, assembler isn't inherently bad, but its use (usually) needs to be restricted by Structured Programming organization techniques.

### State

Computers support *state*.  

Period.

That is what RAM is.  

That is what Disk is.

How can we constrain the use of *state*?

Call a function that returns some value(s).  

Store that value(s) somewhere. 

Wrap the whole process in some syntax that containerizes the state and doesn't let it leak into other parts of the system.

Tune the syntax so that it allows exactly one use for state.

### Flags

Flags are assumed-to-be-bad because unrestricted use of flags has caused many problems.  

We tamed the unrestricted use of global variables.

We tamed the unrestricted use of GOTOs[^cps].

Just about every time that we tamed a hoary concept, we tamed it by *containerizing* it.

We built *containers* using ASCII art, e.g. `{ ... }`.

Now, we can draw diagrams using computers.  There is no longer any need to stick to ASCII art.  Boxes are better-looking containers than brace-bracket characters.

[^cps]: And, we are now un-taming GOTOs by using continuation-passing-style.

StateCharts are one way to containerize *flags* (flags used for tracking state).

### Mutation
### State Machines, StateCharts

[Harel](https://guitarvydas.github.io/2020/12/09/StateCharts.html) figured out how to containerize state.

He tamed the "state explosion" problem.

### History

Computers can sequence events.

Period.

To do this, computers need to remember (store) history.

### Time

To work with History, you need to use a notation that supports the notion of *time* as a first-class entity, or as a default.

Our current programming notations support exactly one kind of history - synchronous, sequential.

Our current notation has synchrony baked right into it.  For example, we use *text* to represent programs and we *know* that lines of text follow each other in synchronous lock-step fashion.

This is OK for some problems[^calc] but not *all* problems, like the internet.

[^calc]: I call this set of problems "calculators".  1-in and 1-out.  All data arrives at the same time.  All data exits at the same time.  If you are building a fancy ballistics calculator, this notation works fine.  If you are building internet servers, this notation needs to be bent to remove unintended synchrony.

### Blocking

Our current notation has *blocking* built right into it.  

CALL blocks the caller until the callee returns.  

Will the callee block, too?  We don't know.  

We've had to hack on our notation to allow for non-locality of blocking.  We call this hack *preemption*.

### Share Memory
### Time Sharing
### Programs as Drawings

## Domains
### Robotics
### IoT
### Blockchain
### GUIs

## Loops, Recursion

Looping and recursion don't make sense in the new reality (distributed programming).

Looping was a knee-jerk, unrestricted concept inserted into languages when we had only single-CPUs and expensive memory.

Recursion is a refinement of Loop.

In a distributed environment, if you want to build a Loop, you simply send a feedback message to yourself.

In a distributed environment, you don't send a stack down a wire.  This essentially negates the use of recursion as a notation for distributed programming[^recur].

[^recur]: You can continue to use recursion and loops as a notation that describes the *innards* for distributed nodes, just not as a notation (language) for describing the interactions *between* nodes.

In single-CPU, shared-memory environments (like computers of the mid-1900s) it was OK to use recursion and loops and we didn't notice that we were notationally boxing ourselves in.

## See Also
      
The [Mars Pathfinder disaster](https://www.rapitasystems.com/blog/what-really-happened-software-mars-pathfinder-spacecraft)

[Table of Contents](https://guitarvydas.github.io/2021/12/10/Table-of-Contents-Dec-01-2021.html)
[Blog](https://guitarvydas.github.io)
[Videos](https://www.youtube.com/channel/UC9EJr0nKHwadbHUtc5zHdmQ/videos)
[References](https://guitarvydas.github.io/2021/01/14/References.html)
[Books](https://leanpub.com/u/paul-tarvydas.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" > 
</script> 