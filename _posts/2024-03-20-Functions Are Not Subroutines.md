CPUs implement subroutines.

Functions are different from subroutines.

Function-based programming (FP, Fortran, Lisp, Python, etc.) might be a convenient *simplifying assumption*, but, it is *only* a simplifying assumption.

Physicists use *simplifying assumptions* all of the time, but, physicists remain cognizant of the limitations of such *simplifying assumptions*, and, physicists switch notations when they bump up against the limits of such *simplifying assumptions*.

Functions in mathematics operate faster than the speed of light - one can perform substitutions on paper in an instant.

CPUs must obey the laws of physics. The CALL instruction takes a certain amount of time to execute. The RETURN instruction takes a certain amount of time to execute. These instructions, both, use a piece of shared memory, called the "callstack". CALL/RETURN was invented to support code-sharing, not *functions*.

There is an impedance mismatch between FTL[^ftl] functions and physical CPUs. Stretching the function-based paradigm over CPU physics is useful in some cases, e.g. creating ballistics calculators for the military, but, can be inconvenient in many other cases, like sequencing events in time (e.g. iMovie, Flash, Garage Band and friends). Function-based notation has no notion of *time* built into it, hence, it is difficult (read: accidental complexity, workarounds, epicycles) to express a time-based operation in a time-less notation. It's not impossible to use a time-less notation for every problem, it's only more difficult than necessary.

[^ftl]: FTL: Faster Than Light

# Other Points To Consider

## Determinism - Synch vs. Asynch
- step-wise simultaneity only gives the impression of asynchronous behaviour because it happens fast enough to fool the human brain

## Shared Memory vs. Reentrancy
- CPUs are inherently non-reentrant, they have one set of - shared - registers, one blob of - shared - RAM, etc. 

## The Original Model of CPUs Was Single-Threading
- Hardware designers designed CPUs with the idea that one CPU would be used for each thread 
- But, in the 1950s, this was too expensive, so human-time was wasted on developing multi-tasking and time-sharing
- In 2024, CPUs are no longer expensive, CPUs are cheap enough that we can afford to throw one CPU at each thread.

## Race Conditions
- There is only *one* race condition in physics - did two events arrive "at the same time?"
- This race condition is caused by a sampling rate that is too slow
- The obvious fix for this race condition is to use faster hardware and sensors
- A less-obvious fix is to accept events in any order then put them back in some sort of order that the rest of the software can deal with
	- if A arrives before B, you must wait for a B before proceeding
	- if B arrives before A, you must wait for an A before proceeding
	- does the rest of your software deal with the possibility that more than one A-event arrives before the next B-event (or v.v.), or, does the rest of your software avoid that kind of case and declare it to be "undefined"? 
		- both answers are acceptable, if clearly stated.
- Every other kind of "race condition" is just accidental complexity
	- typically caused by tripping over your own feet due to the over-use of shared memory

## Preemption vs. Mutual Multi-tasking
- preemption is a symptom of the over-use of the function-based paradigm
- preemption is used by most operating systems to fake out re-entrancy by swapping out one set of shared CPU registers for another set of shared CPU registers, likewise for shared RAM, etc.
- handling preemption is inefficient - it requires extra software that isn't needed in a single-threading model
- pre-emption is only needed by developers, not end-users
	- developers use expensive development hardware and expect that expensive hardware to help them catch bugs during development
	- end-users only need preemption when developers sell them buggy software
	- end-users are happy with a "game cartridge" mentality
		- if you fake out "game cartridges" in software by using preemption, the result can still be fairly simple

## Simplifying Assumptions For Time-Relative Events
- simplifying assumption: we don't need to know absolute time, just relative time between events
	- e.g. event A came before event B
	- easy if fan-out is prohibited
	- harder - but, quite convenient - if fan-out is allowed
		- atomicity
			- possible on single CPU
			- impossible in distributed systems
				- due to noticeable latencies
				- invent new *simplifying assumption(s)* ?
			- simplest form
				- stop the world, deliver event to all receivers
			- simplest form can be optimized
				- make explicit which receivers receive which events 
					- i.e. "on the same net"
					- a "net" goes from one output to a number of receivers (N)
					- if N > 1, stop everyone on the same net
					- if N = 1, it doesn't matter
						- no receivers need to be stopped
								- as long as the enqueueing operation is atomic itself
				- don't stop the world, stop - if necessary - only the (smaller) group of receivers for a specific event, the rest of the world can carry on
- fan-out means one output feeding more than one input
	- in hardware, fan-out means tapping off a small (insignificant) amount of current from the source and feeding it to another sink
		- impedance calculations tell you when you can get away with this *simplifying assumption* and when you can't get away with it
	- in software, fan-out means copying, 
		- or, pointer-passing where copy-on-write is enforced
		- atomic delivery of events is convenient
			- e.g. if event A is sent before event B, *all* receivers see A before B, no interleaving or reordering
	-  fan-out is *necessary* to allow abstraction of modules
		- i.e. the ability to reduce the number of ports on a module by bundling many ports into an apparently-single port 

## The Right Way to Handle Asynchronous Processes - Protocols
- protocols, not low-level, step-wise simultaneity
- most current languages synchronize at a very low-level
	- hence, difficulty in dealing with async, 
		- e.g. plethora of workarounds: callbacks, promises, .then, futures, etc.
		- e.g. writing ethernet driver stacks is painful using most current programming languages
	- top-down, left-to-right sequencing of statements
		- akin to assembler, but, slightly less verbose (aka "higher level")
	- over-use of synchronization causes gotchas
		- hidden coupling results in spooky action at a distance 
			- one change can break everything in unexpected ways
		- Mars Pathfinder fiasco led to the invention of a new, ad-hoc workaround
			- called "priority inheritance"
- blockchain
	- truly distributed
		- nodes can drop-in and drop-out of the system at any time
		- pBFT is basically a very simple state-machine based protocol wrapped onto some crypto

## True Asynchronousity Implies FIFO Queues
- nodes need to "run at their own speed"
- use one input queue for each node
	- allow the node to work at its own pace without needing to synchronize with the sender 
- use one output queue for each node
	- to break synchronous chain of event delivery
		- depth-first chain of event delivery happens once in a while
			- over-synchronization of event delivery chain
		- depth-first chain of event delivery happens all of the time with CALL/RETURN based language implementations (e.g. most current programming languages, Rust, Python, etc.)

## Ethernet Performs No Synchronization, Whatsoever
- ethernet - at the hardware level - does not synchronize
	- node uses "random back-off" strategy
		- node monitors its own output
			- if output is garbled, it means that contention has occurred
				- the node "backs off" and tries again later (milliseconds later, microseconds, nanoseconds?)


# Appendix - See Also

### References

[references](https://guitarvydas.github.io/2024/01/06/References.html)

### Blog
[blog](https://guitarvydas.github.io/)

### Blog
[obsidian blogs](https://publish.obsidian.md/programmingsimplicity) (see blogs that begin with a date 202x-xx-xx-)
### Videos
[videos - programming simplicity playlist](https://www.youtube.com/@programmingsimplicity2980)
### Books (WIP)
[leanpub](https://leanpub.com/u/paul-tarvydas)
### Pamphlets
[A DSL For Writing DSLs](https://tarvydas.gumroad.com/l/hiypq?_gl=1*1kki8v2*_ga*NTI5MDkzNTI0LjE3MTAzNTQzNjU.*_ga_6LJN6D94N6*MTcxMDg2NDAyNy41LjEuMTcxMDg2NDAyOC4wLjAuMA..)
[Wond'ring Aloud: Is Concurrency Difficult?](https://tarvydas.gumroad.com/l/dvtej?_gl=1*o7hy6z*_ga*MjA0NzUyMDY1Mi4xNzA3NDc3MDIx*_ga_6LJN6D94N6*MTcwNzQ3NzAyMC4xLjEuMTcwNzQ3NzI5Ni4wLjAuMA..)
### Discord
[Programming Simplicity](https://discord.gg/Jjx62ypR) all welcome, I invite more discussion of these topics, esp. regarding Drawware and 0D
### Twitter
@paul_tarvydas

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
