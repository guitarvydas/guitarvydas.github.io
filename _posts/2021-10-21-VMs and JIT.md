---
layout: post
title:  "VMs and JIT"
---

Node.js and JRE are apps that run at "runtime" and read/load/run the JS/Java code.

JDK is optimized by breaking it into 2 pieces - the dev stuff and runtime stuff.  If you don't need the dev stuff, you can save memory by not loading it.

Let's pick on JRE[^beam]:

[^beam]: This discussion also applies to other VMs like Erlang's *Beam*.

JRE runs some .java app. 

How? 

# VM

The VM is an app that reads the .java code and executes it (in other words, it "interprets" the code).

There is a way to optimize execution, so that it takes less time:
1. convert the .java code into some intermediate form
2. define an API for the intermediate form
3. write an app that understands and runs all code written in the intermediate form.

The intermediate form (2) is called VM (Virtual Machine) *bytecodes*.

Specific calls to the VM API are done using short codes called *bytecodes*.

App (3) is the VM.

Most often the VM *looks* like an assembler-runner (interpreter).  The API *looks* like assembly instructions for a ficticious machine.

A *compiler* is just an app that pre-processes code as in (1). In the end, *all* code is interpreted by the hardware CPU.

We used to use *Assemblers* to do step (1), then, we discovered that syntactic sugar could make the code less onerous to read (for humans).  

This led us to building apps called *compilers* and replacing *assemblers* by these new-fangled apps.  

Then, we discovered that OO was a good way to organize syntactically-sugared code.  

Then, we discovered that we could do better with even *more* syntactic sugar and we invented type-checker apps and FP[^1].

## Example

For example "hello('xyz');" is a string.

The runner interprets the string each time - 13 characters, plus some sort of stop character or a string length.

The runner doesn't know how long the string is, so it must walk the string from front to back each time.

We can "optimize" the string by pre-processing it.  If we do this right, the runner will have less work to do, and, will take less time to run the program.

Let's say that we use code `0x50` to mean "call function", code `0x61` to mean push string onto the string stack (we invent a stack and build it into the VM) and `0x75` to mean push the address of a function onto the function call stack (again, built into the VM.  Most VMs use just one stack for, both, strings and function addresses, but that's so 1950's).

We might compress the above function call as:

```
0x61 "xyz"   // hash string "xyz", and push its index (hascode) onto the string stack

0x75 "hello" // find the function hello and push its address onto the function stack

0x50         // call function (with one argument)
```

The runner can eat this stuff up faster than re-processing "hello('xyz')" each time, so, we have achieved the goal of making our program run faster.

The pre-processor is a *compiler*.  

The runner is a *VM*.

We run 2 apps

1. First, we run the *compiler* app, then

2. We run the VM app (which eats our bytecodes and runs them).

If we run the *compiler* at *VM* time (called "runtime"), then the *compiler* is called a *JIT* (just a name change (maybe a philosophical change, too (TL;DR)).

I doubt that the Java VM uses the same codes as I used in this example.  You can see the actual codes decided upon by the Java VM inventors in the Java VM documentation.

[^1]: IMO, FP goes "too far" and tosses the baby out with the bathwater, but that's for another discussion.

# JIT

JIT - Just In Time compilation - is nothing new (it was invented in early Lisps, and was explored more deeply in the *Self* language).

JIT is a bundled app that includes the *compiler* and the *VM*.  Instead of pre-processing code as in step (1), we defer the pre-processing until step (3) and do the work on an as-needed basis.  The first time we need to call a function, we interpret it *and* we compile it.  Then, when we come across the same function again, we just use the compiled version.

This combination *can* run faster if the code contains lots of unused code - the *compiler* compiles only the bits that are really needed. 

Instead of writing the bytecodes out to a `.o` file, a JIT compiler does the work in-memory and makes the result available during the run.

If you need to run the final app many, many times, it might be faster to pre-compile it only once instead of JIT'ing it every time you run the app.

# Takeaways

A compiler is just a pre-processor which compresses code into some more convenient, normal form that, hopefully, runs faster.

We have learned how to build better checking into our compilers.

1. We use syntactic sugar (which causes us to build parser apps), and,
2. We use type-checking, but, the cost is that we need to modify the languages. For example, it is possible to write better (more complete) type-checking for a Haskell program than for a C program, but the programmer has to follow the rules of Haskell when writing code. [*Q: Is it worth it to use a very-high-level language like Haskell instead of C or assembler?  What are the trade-offs? (Big-time efficiency gains don't come from switching languages, they come from switching designs.)*]

A compiler is merely an app.

A VM is merely an app that loads and runs programs.

JRE is Java's VM.

JDK is the JRE plus a bunch of dev-oriented apps.

The JRE, JIT'ed or not, boils down to running the CPU's API - called *opcodes*.

The CPU *interprets* opcodes. 

Always.  

[*Corollary: every app is an interpreter.  This means that compilers are interpreters, too, but we don't think of them that way. Less clutter in the brain means more space for higher level thinking.*]

Assemblers are cave-man era compilers that translate text into *opcodes*.  (As always, there is more nuance and detail, but TL;DR).


# See Also

[Blog](https://guitarvydas.github.io)
[Table of Contents as of Sept 17, 2021](https://guitarvydas.github.io/2021/09/21/Table-of-Contents-Sept-17-2021.html)
[Videos](https://www.youtube.com/channel/UC2bdO9l84VWGlRdeNy5)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
