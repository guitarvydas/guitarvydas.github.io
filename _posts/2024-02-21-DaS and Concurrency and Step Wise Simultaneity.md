I firmly believe that "language" affects thinking.  

Changing the "language", the point of view, will enable us to imagine new kinds of things and solutions. 

To me, it is obvious that the ideas of "operating systems" and "concurrency" expressed in functional notation result in major bloat. 

That kind of bloat is not merely materialistic - i.e. how many bytes are wasted, how much CPU time is wasted - but, it is also a waste of human intellect. 

Everyone - except programmers - knows that if you want to do 2 things in parallel, you enclose them each in black boxes and then arrange the black boxes to be beside each other instead of being arranged in a linear sequence. Any CEO will draw it that way on a whiteboard. Yet, programmers have over-complicated this concept by trying to treat it in linear form. You need several years of University training to understand the gyrations invented in Computer Science to explain the simple concept of concurrency. 

To get philosophical, if you believe in "free will" then you understand that you can *never* express true concurrency in linear terms. Yet Computer Science tries to express concurrency in a step-wise manner (and will never achieve this final goal). 

Popular forms of CompSci slap the name "concurrency" onto something that is not true concurrency. Research into networking has the right idea - create explicit protocols between things that have free will. 

Instead, C/C++/Rust designers build synchronous protocols deep into the bowels of their languages and, therefore, cut off avenues of thought. 

Yes, it seems that a fruitful way to rustle jumbled electronics is to sequence it and to put it into black, epoxy boxes with specific APIs (ICs and opcodes, resp.), but that is not true for programming language design. In that sense, C/C++/Rust/Haskell/etc. are all the same and are all very low-level. 

Prolog is different. 

Distributed programming, robotics, gaming, GUIs, etc. are different, too. 

We don't really have languages for dealing with distributed programming in non-linear ways. We have libraries - called "thread libraries" - that let us assemble (as in "assembler") solutions to distributed problems, but, we don't have languages that let us express such concepts in high-level form. Duct-taping constructs like "par" onto sequential languages is but a work-around to a more fundamental problem.

I've invented a new syntax for expressing true concurrency, as opposed to the step-wise sequential syntax that is required by popular programming languages. My compilers must map that syntax onto existing sequential hardware, but, that's just a minor practical issue at this moment. 

I'm calling the syntax DaS - Diagrams as Syntax. The compilers must use 0D principles to translate DaS into sequential opcodes in low-level languages like C/C++/Rust, etc. I claim that this syntax is very good for programming at the "function level" as we call it.

A major difference is that DaS uses 2 fundamental operations, whereas popular programming languages use only 1 fundamental operation. DaS uses, both, CALL/RETURN and SEND/RECEIVE, whereas popular languages provide only CALL/RETURN. 

And, DaS defaults to a paradigm where everything is asynchronous to begin with, whereas popular programming languages default to a paradigm where everything is synchronous to begin with. The latter approach necessitates the use of work-arounds when solving truly concurrent problems, work-arounds such as preemption, operating systems, thread libraries, etc. 

And, DaS forbids memory sharing by default, whereas popular programming languages downright encourage memory sharing. We see that this causes problems and has caused the invention of edicts like "assign once" and "no mutation". 

The syntax for subroutine calling in popular languages looks suspiciously similar to the syntax for writing functions in mathematics, but, they are not the same, a fact which has been causing gotchas and invention of ad-hoc work-arounds for decades. For example "thread safety" is a moot concept if memory sharing is prohibited at a fundamental level.

How are subroutines different from mathematical functions? Subroutines take time to execute. Mathematical functions take no time at all. Mathematical functions are mappings, not step-wise sequencings that take time. In essence, mathematical functions work faster than the speed of light, whereas CPU subroutines have to obey the laws of physics. This impedance mismatch - caused by thinking that subroutines are the same as mathematical functions - has been causing gotchas and the further invention of edicts that constrain the use of CPUs. 

RAM supports mutation. Proclaiming the edict "no mutation" restricts the full use of the powers of RAM. In the eyes of many people, this restriction is useful - physicists call this kind of thing "a simplifying assumption" - but, it is a restriction nonetheless. Furthermore, the real world involves mutation. Sticking to a single notation that strictly prohibits mutation, ignores reality. 

Function-based notation is useful, but it is not the end-all-and-be-all.

We can question and observe the limits of our current programming notation. Anything that seems to be difficult is probably difficult due to the notation. Everything is difficult, but, everything can be understood and expressed in simple terms using a suitable notation.

For example, today, most programmers roll their eyes when faced with thoughts of concurrency and just avoid the issues. Fiascos, like call-backs, promises, futures, etc. make this simple concept appear more complicated than it needs to be. This is a *tell* that the function-based notation is being pushed beyond its sweet-spot. We can keep pushing and groaning, or, we can simply switch to a better notation, while continuing to use the function-based notation where it is appropriate and more concise. The only fully FP programming language that I have seen is Tunney's Sector Lisp (and, probably BLC, but, I know less about BLC). Languages like Haskell claim to be FP, but make concessions for concepts beyond the reach of FP notation - like  mutation and heaps and garbage collection, etc. Sector Lisp is pure FP, whereas Haskell is not pure FP (!). The problem with Haskell and other languages of that ilk, is that they try to be everything to everyone, instead of just sticking to the knitting. You can't stuff assignment and mutation and side-effects into a language that only handles pure functional thinking without playing whack-a-mole. 

The fundamental problem is the idea that there must be "one language to rule them all". Instead, we need many languages and a way to bolt them together. Compiling languages that are the same into an IR that is the same, isn't the full answer.  If you want to build a language that is different, begin with the assumption that everything is asynchronous and not sequenced. If you have to translate that assumption to a step-wise IR, then so be it, just don't build that assumption into the HLL language.

Most people think that the use of multiple languages is a bad idea. Most people think that the use of VPLs is a bad idea. Most people think that Actors don't work. I suggest that these opinions have been formed by exposure to bad implementations of these ideas. Step-wise, overly-synchronized implementations of these ideas leads to poor experiences.

# Key Aspects
## 0D - Call and Send
As mentioned above, the basis of 0D is the addition of `send ()` to programmers' repertoire.

This isn't enough, since `send ()` requires programmers to arrange systems in layers. If they don't use such arrangement, they will encounter scaling problems later. Flat-ness creates confusion as systems grow larger in size.
## Structured Composition

This is the second aspect that is required for this technique to work and to scale to larger systems.

Components can have multiple outputs and multiple inputs. This is difficult - but not impossible - to express in textual form.

Using diagrams - DaS - makes it easier to express and to read code that contains multi-input and multi-output components. I find it much easier to read source code for this kind of thing in diagram format than in pure textual format. Note that *diagram format* is a hybrid of diagrams and text - it is not all-or-nothing. This format is not solely composed of diagrams and it is not solely composed of text.

Until recently, it seemed overly-difficult to use diagrams as code and to compile diagrams to executable binary.

I show that this is "easy" to do, using OhmJS to parse XML produced by diagram editors. In this specific case, I used `draw.io` which creates `.drawio` files in `mxGraph` format. `MxGraph` is a variant of XML. It is textual and can be parsed using existing tools.

A specific example of doing this is the Odin-based `0D` repository https://github.com/guitarvydas/0D . Contact me if you have questions / comments about this code.


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
