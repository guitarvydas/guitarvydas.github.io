In a computer - actually a REM (Reprogrammable Electronic Machine) -  the construct called a  "function" is a subroutine that has no other side effect other than taking time and returning a value based upon the inputs.

I argue that there is a religion-based pressure to transform "computer functions" into "mathematical functions", and, that this is a dangerous approach. REMs are something new. Mathematical notation is old and geared towards expression on papyrus and clay tablets. REMs operate in four dimensions in accordance with the laws of physics, whereas mathematical notation is fundamentally two dimensional and makes the simplifying assumption that some of the laws of physics can be ignored.

Iverson states this position clearly by saying "The preceding sections have attempted to develop the thesis that the properties of executability and universality associated with programming languages can be combined, in a single language, with the well-known properties of mathematical notation which make it such an effective tool of thought." in the conclusion to his paper [1979 Turing Award Lecture - Notation as a Tool of Thought](https://www.eecg.utoronto.ca/~jzhu/csc326/readings/iverson.pdf). I suspect that many others also believe in this agenda, whether sub-consciously or overtly.

I argue that the current model of "computers" is based on the *mathematical* definition of "function" - and - is bumping up against an asymptote that *invalidates* the basic simplifying assumption. In fact, just the name "compute-er" for Reprogrammable Electronic Machines belies the strong underlying agenda to transform REMs into devices based solely on *mathematics*.

The function-based simplifying assumption is useful, but, is limited in scope.  The simplification doesn't hold water when considering other actions that REMs can accomplish. 

The best realization of function-based programming is visible in Sector Lisp (and BLC), which simply *blows away* all other so-called FP languages by being 10x smaller than the nearest competitor. The Sector Lisp GC is a mere 40 bytes - better than even McCarthy's GC. This smallness is due to the strict application of functional programming principles to the problem.

If, as I do, you hold Sector Lisp up as a golden standard for functional thinking, you see a glaring problem. The notation cannot actually accomplish anything, since - as the functional programming edict dictates - it doesn't allow mutation. 

This does *not* mean that we have to shove mutation into Sector Lisp, it merely means that we need to make Sector Lisp co-exist with other notations. Programmers could use functional programming only where the simplifying assumption applies, but, might use something else when functional-programming notation becomes maxed out. 

Our current religious belief, that everything must be crammed into a single programming language, prevents us from thinking about using multiple notations and thinking about simply bolting the multiple notations together into a final program. A union of programming notations into a single unified notation *cannot* be as laser-focussed on specific aspects of a problem as specific, single-target notations can be. DSLs are on that path, but, we can do even better. I call those "SCNs" (Solution Centric Notations). Generalization ain't as good as specialization. General purpose programming languages can't be as good as very-specific programming language-lets. 

The "giants" of programming are generally mathematical notation worshippers. It appears to me that they are twisting Reprogrammable Electronic Machines to conform to the image of mathematical notation instead of dealing with the realities of REMs themselves and fitting a (new) notation to the realities of REMs. It seems to me that all of the "rules" of FP are geared towards tamping down the true abilities of REMs to make them fit a pre-existing notation designed for clay tablets and papyrus. Harel's Statecharts and, even, Denotational Semantics, at least, attempt to deal with the realities of REMs, while edicts such as "no mutation", "referential transparency", "control flow and data are the same", "determinism", etc. are forcing non-reality onto the application of REMs. From my perspective, so-called "Computer Science" has become a science of *applying* REMs to compute-ing, instead of being a science *about* REMs. 

The realities of REMs are concretely different from the ideas of scribbling equations down on paper.

"Standing on the shoulders of giants" works only when the giants are solving the same problem that you are.

Mathematical notation is easily handled by Lisp-style macros, i.e. referential transparency of text at "compile time". The idea of forcing such mathematical notation into a single time-less notation, and, executing that one-size-fits-all notation on REMs, has caused a great deal of angst and anti-simplicity.

I suspect that the pain won't go away until Reality is acknowledged.

What is being missed is that compute-ation isn't enough. The fact that one result is the same as another is *not* sufficient for the analysis of REMs. Something more is needed. We see "tells", but, ignore them - e.g. the invention of preemptive operating systems that fake out imaginary multiple CPUs that - anti-realistically - share memory, the ad-hoc invention of workarounds like priority inheritance, the increasing bugginess of hardware as the field of hardware design adopts "software" techniques, etc.

- A CPU is just a chip. You bolt it to another chip(s), RAM or ROM, and you get a step-wise sequencer that interprets opcodes stored in RAM/ROM. The fact that opcodes happen to be stored in RAM/ROM does not mean that the interpreter is the *same* as other data stored in RAM/ROM.
- The classical Turing machine misses addressing one key feature. It takes time to move the tape back and forth. Instead, mathematical notation worshippers discard this inconvenient detail and look only at the result of the compute-ation, and, get into trouble, because the act of compute-ing the result by moving the tape back and forth causes little gotchas in the process of compute-ing the result.
- CD (Continuous Delivery) has sprung from a culture of producing buggy products. A bug in the code is the same as a bug in the design, from the perspective of end-users. 
- Nobel Laureate Ilya Prigogene ("Order Out of Chaos"), also, decries the over-use of simple mathematical notation whilst ignoring the irreversible direction of time. Prigogene states that functional thinking has retarded Physics by 100 years.
- Most programming languages (like Python, Rust, Javascript, etc.) are predicated on the notion of step-wise compute-ation instead of truly asynchronous operation, i.e. they imply top-down-left-to-right sequentialism, instead of free will and nodes running at their own speed.
- Programmers and researchers ignore the real goal - to make machines helpful to end-users. Instead, the focus is on guaranteeing sound mapping from *programmers*' ideas of what end-users want, regardless of whether the result satisfies end-users and is robust from the end-users' perspective. Consideration for end-users is relegated to airy-fairy notions like requirements documents, Agile, etc.
- The focus is on Waterfall development, instead of on iterative development. Iterative development spirals in towards acceptable solutions. You can't predict what the solution to a problem will be unless you fool around and fail at it a few times. Even Brooks said that. Instead we build notations and tools that support only a non-iterative development process, i.e. waterfall thinking.
- Normal people use diagrams, yet, programmers insist on using only text. Obviously, this is a deep disconnect. Diagrams, though, tend not to work so well when problems are reduced by sequentialism. We've seen this in the apparent failure of programming-by-diagram tools (UML, LabVIEW, Scratch, etc.). Instead, we see concerted efforts to write programs in text, then, to re-express the programs in diagrammatic form as second-class citizens. A minor fix is all that is required to allow programming-by-diagram, but, this fix is essentially invisible to those steeped in the evil-Borg, micro-management, over-sychronization myth who think that everything, including reality, can be expressed in deterministic forms.
- The limits of the simplifying assumption - time-less notation - have been reached and different notations need to be used to express further capabilities of REMs. Building new notations based on top of the already maxed-out function-based notation can only result in accidental complexity and epicycles. Thinking *out* of the box is required, instead of continued labour to think *inside* the box. A way to approach this is by using the concept of [first-principles thinking](https://guitarvydas.github.io/2022/05/25/Programming-First-Principles-Thinking.html).
- The "answer" is to admit that free will - asynchronousity - exists, and to begin to deal with that reality. Networking research is on the right path. `*NIX` pipelines are on the right path, Statecharts are on the right path. You can control the innards of a single node synchronously, but, you can't deal with a network of nodes in the same way, especially when latencies become noticeably long and perceptible on human timescales.  I argue that it is much simpler to push asynchronous thinking down to the program subroutine level and to discard all ad-hoc accidental complexities concerning re-entrancy, preemption, etc.
- In the 1970s, I - as a poor student - built a machine that was capable of running programs and, even, capable of running a compiler in about 22K of RAM- for only a few hundred dollars. Today, my 99 year old mother needs to pay more than that and needs Mbytes of storage just to be able to play Tetris. Something is wrong with this picture. We're measuring success in a wrong manner. It used to be thought that 640K of memory space is all that you need, but today, if you don't have 512G of SSD, f'get about it. Granted, we store pictures that contain many more pixels than picture capacities in the 1970s, but, our software has, also, bloated enormously with no honest gain in utility and simplicity to the end user.
- Measurement of success is based on mathematical beauty instead of end-user utility and robustness. Computers are certainly not more robust in 2024 than they were in the 1970s. We needed to power down machines after use in the 1970s and we still need to power them down after use today, 50 years later. My Mac claims to have a Sleep mode, but, if I don't preventative-reboot it at least once a week, I begin to get strange behaviour and loss of work.
- The main tenet of Science is to "fail fast", i.e. to relentlessly attack a theory and to prove that it is wrong before it spreads. You can't prove a theory to be correct with a single data point, but, you can prove a theory to be incorrect with a single data point. A good scientist provides enough detail for replication and provides the theory in falsifiable form. I think that 50 years of piece-meal workarounds (aka "epicycles") and the increase in bloat and the current state of brittleness of software are enough evidence to show that our current approach is broken. We require a very fresh new approach to the issues. Current ideas in FP are pointing towards the idea of "no mutation". Taken to its limit, that means that multitasking, which is based on shared memory and mutation, needs to be deeply rethought - adding baubles and workarounds to our current notation is not good enough.
- Sector Lisp is the only example I've seen of pure FP code, even better than McCarthy's code.
- To be Scientific, a theory must be falsifiable. What is the (or, at least, what is just one) falsifiable theory in Computer Science?  I would say that the main goal should be "end users can use computers that are more robust and cheaper than before". This is clearly false - for example, I have to perform a preventative reboot of my Mac at least once a week, and, I paid essentially the same amount, taking net present value into account, for my Mac than for my first computer. Apps are way more bloated than they used to be. I am faced with new vectors for criminal attacks than I used to be. Granted, data is much larger, but, that does not directly permit associated app bloat. Bloat costs end-users `$`s. It appears that the only falsifiable theory in computer science is accepted to be "things become easier for *developers*" whilst ignoring end users. I believe that this is the wrong basis for measurement of success. I believe that the way to re-address these problems is to apply "first principles thinking" (remembering what a CPU is and what a CPU isn't).
- "Making things easier for developers" is but a sub-goal in aid of achieving the uber goal directed at end-user robustness and cost. Programs used to be small and simple. Today, programs are anything but small and simple. Attacking larger problems does not *need* to imply gluing bits of text together by inventing epicycles like "imports" and "colorization" and "monads" and ".then" and "re-entrancy", etc.
- The only fully-FP programs I've seen are Tunney's Sector Lisp and BLC. Even McCarthy didn't achieve the smallness of Sector Lisp and pure FP. Furthermore, it is clear that gluing band-aids onto mutational notations and calling the result FP isn't working out so well - when measured against the uber goal. 
- Users are forced to pay for the privilege of Q/A'ing buggy products sold to them by developers who feel entitled to release buggy, poorly designed apps, due to the use of technologies like CD (Continuous Delivery). Users are forced to pay for bloated operating systems that protect buggy apps from one another.
- Theorem provers are nice, but, I see no evidence that they actually result in achieving the uber goal. ChatGPT is nice, but it ain't Engineering. ChatGPT makes things up ("hallucination") and can't be relied upon.
- Chips are designed using totally asynchronous components. Software is designed using totally synchronous components.
- Chip manufacturers put guarantees on their products. Software manufacturers hide behind  EULAs written in fine print.
- So-called Computer Science is more like the science of transforming mathematical notation into the discrete (quantized) realm, kinda like FFTs vs. analog. 
- If I assume that the word "computer" refers to the concepts of Reprogrammable Electronic Machines, then I would say that so-called Computer Science misses the mark of addressing the problem space of REMs and, instead, addresses only the problem space of transforming mathematical notation into the discrete (quantized) realm, kinda like FFTs vs. analog.
- I think that there is a sub-conscious agenda to warp REMs (Reprogrammable Electronic Machines) until they fit neatly into mathematical notation. This is belied by the name given to such an idea - compute-er.
- CALL and SEND are orthogonal operations. Both are necessary, but, the myopic focus on function-based notation has essentially disappeared SEND. At best SEND is given second-class status. SEND is expressible in functional notation, but, is *not* a basic part of the notation.
- The religion of function-based programming attacks a problem which once did exist, but, no longer exists - the high co`$`t of CPUs. Hardware in 2024 is *very* different from hardware in 1950. Today's hardware can display scalable, overlapping graphics instead of just struggling to display small, fixed-sized bitmaps in a strict, non-overlapping grid arrangement. We no longer need be concerned by issues of re-entrancy and time-sharing and memory-sharing and so-called "efficiency". Dealing with these issues creates software bloat and inefficiency. Most applications don't need to be concerned with these issues. All apps, though, invisibly pay a tax to solve these problems even when such problems aren't of concern.
- Electronic engineers use a perfectly good notation - chips connected to other chips by lines. This notation is fundamentally asynchronous, yet, sufficiently powerful to build scalable systems. This notation was subverted by the inclusion of synchrony at a very low level resulting in 50+ years of discovering gotchas in an ad-hoc manner.
- This is not *only* mathematics. This is something new. Yet, we continue using an old notation to deal with this new concept(s).

# Further
[Computer Science Is Not About Computers](https://guitarvydas.github.io/2024/03/26/Computer-Science-Is-Not-About-Computers.html)
# Appendix - See Also

### References

[https://guitarvydas.github.io/2004/01/06/References.html](https://guitarvydas.github.io/2024/01/06/References.html)

### Blog
[blog](https://guitarvydas.github.io/)

### Blog
[obsidian blogs](https://publish.obsidian.md/programmingsimplicity) (see blogs that begin with a date 202x-xx-xx-)
### Videos
[videos - programming simplicity playlist](https://www.youtube.com/@programmingsimplicity2980)
### Books (WIP)
[leanpub](https://leanpub.com/u/paul-tarvydas)
### Pamphlets
[gumroad](https://tarvydas.gumroad.com/l/dvtej?_gl=1*o7hy6z*_ga*MjA0NzUyMDY1Mi4xNzA3NDc3MDIx*_ga_6LJN6D94N6*MTcwNzQ3NzAyMC4xLjEuMTcwNzQ3NzI5Ni4wLjAuMA..)
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
