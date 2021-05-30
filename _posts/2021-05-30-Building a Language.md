---
layout: post
title:  "Building a Language"
---
One of the first things I learned in computing was how to build a language.

I sight-read Frits van der Wateren's Lisp 1.5 into my machine (translating from MC6800 to Z80 opcodes on-the-fly).

Then, I implemented the Lisp compiler in John R. Allen's book "Anatomy of Lisp"[^1].

I compiled the `iota` function - my machine had _just enough_ memory to house the compiler plus the source code for `iota` plus the compiled version of `iota` to run the function.  I saw that, indeed, the compiled version ran much, much faster than that interpreted version.  I saw that the compiled version didn't garbage collect as often as the interpreted version.

Then, DDJ came out with the SmallC source code. "Open Source" was not in vogue at the time, so it was a pleasant surprise to get my hands on actual source code to an actual compiler. I hadn't even heard of C before that time.

My friend - Chris Lewis - and I typed _all_ of the source code for SmallC into a PDP11 (at UofT's CSRI) during one evening. At around 2am, I tried the "smoke test". I ran the compiler. I used a very simple test, something like
```
a = b + c;
```
and SmallC printed out the assembly code for the statement (it included the original C source code as a comment), something like 
```
; a = b + c;
MOV L,(name of b)
CLR H
MOV C,(name of c)
CLR B
DAD B
MOV (name of a),L
MOV (name of a + 1),H
```
[That says: move b into register L, zero out register H, move c into register C, zero out the B register, 16-bit add[^dad] registers BC plus HL and put the result into HL, move the bottom byte of HL into *a, move the top byte of HL in *(a+1). (H means "high" and L means "low".  HL combines two byte registers into one 16-bit register.  BC combines two byte registers, B and C, into one 16-bit register.]

[^dad]: It was called double-add!

This was eye-opening, for me. I immediately saw what a program that writes programs could do for me.  Since then, I've been attracted to programs that write programs, e.g. compilers, lisp macros, etc.

[^1]: Warning - the code in the book is not perfectly correct. My copy of the book has pencilled annotations on what needed to be fixed.

# Practice, Practice, Practice
Q: Violinist: "How do I get into Carnegie Hall?".

A: "Practice".

Q: Who originated the concept of Ice Wine?

A: Germany.

Q: Why is Ontario's, Canada, Ice Wine better than German Ice Wine?

A: Practice.

[Background: To qualify for ice-wine status, you need to pick frozen grapes after 3 days of steady -8C weather. In Niagara, Ontario, Canada, each year brings 3 days of -8C weather.  In Germany, this only happens about twice a decade. Q: Why does anybody choose to live in Ontario, Canada?]

Build many notations, several a day, and you will become better at it.

Corollary: Build one language+compiler every year or so, and, you will learn slowly, at best.

# See Also

[Frits van der Wateren Lisp (by permission)](https://github.com/guitarvydas/frits-van-der-wateren-lisp)

[Learning About Compilers Quickly](https://guitarvydas.github.io/2021/03/18/Learning-About-Compilers-Quickly.html)

[8080 Assembly Manual](https://altairclone.com/downloads/manuals/8080%20Programmers%20Manual.pdf)

[References](https://guitarvydas.github.io/2021/01/14/References.html)
[Table of Contents](https://guitarvydas.github.io/2021/05/14/Table-Of-Contents.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
