---
layout: post
title:  "The Software Atom"
---

I think that finding the atom of software is important.

If we find the Atom, then we can construct interesting "molecules" using it, like Programming Languages, IDEs, Programming Notations, etc.

# The Relation

I currently think that triples are The Atom.

I think that relations are triples.

Lisp sexps are triples - `(rel subject object)`.

Javascript Object are triples - `{relation: r, subject: s, object: o}`.

Curried functions are just triples in disguise - `(rel subject) x object`. 

## More of the Same
Everything else is just "more of the same". 

### More Is Better?
More must be better, right? 

Uh, not if _more_ obscures the base truth.

# Writing Code That Writes Code
"Give a man a fish, he eats for a day. Teach a man to fish, he eats for a lifetime".

Our ideal should be to write code that writes code.

Compilers write code.

As it happens, compilers were our "way out" of writing assembler. Compilers write assembler for us. We don't have to write assembler anymore.

# Transpilers
Okay, so we have all sorts of compilers.

What's next in software evolution?

Code that writes code.

We need to write code that writes Python[^1] for us.

We need to write programs that write programs for us. These programs should produce any language we want. 

In compiler-lore, that's called _portability_. We need to write programs that write Python for us.

We already know how to build portable compilers (I'm familiar with Cordy's OCG technology and with Fraser-Davidson's RTL (used in gcc) (See the References section)).

We should be building compilers that create programs in any 3GL we want - transpilers.

We should just hit a switch and get Python code, or Javascript code, or HTML code or Haskell code, or ...

That's called _portability_.

[^1]Or, any language, like Javascript, HTML, Haskell, etc.

Have we seen this already?

We've seen the buds of this concept in `*script` -> Javascript. But, each `*script` is a separate program that is not very generalized.

We've seen the buds of this concept in heavy-duty macro processing, like Lisp macros (compiler built into the compiler).

We've seen the buds of this concept in UNIX command-line tools (they can manipulate text as long as the text is arranged in line-oriented format).

JSON, ASON, etc. are all barking up the right tree.

# Normalization
Q: What happens if you know what a software Atom is and you normalize _all_ software into Atoms?
# Projectional Editing
IMO, Projectional Editing is just more whack-a-mole.

If _all_ software was expressed in terms of Atoms, then Projectional Editing would be a nothing-burger.

# PEG

PEG technology lets us convert notations into other notations easily.

PEG is kinda like REGEXs on steroids.

Q: What conversion would we want?

A: Any notation -> Atoms.  Atoms -> any notation.

## Ohm-JS

Ohm-JS, and, especially the [Ohm Editor](https://ohmlang.github.io/editor/) are currently my favourite form of PEG.

Ohm has warts, but then QWERTY has warts, too.

The Ohm Editor makes it _easy_ to build notations (Languages, etc).

# Toolbox Languages

Some languages are better targets for transpilation than others.

Good languages - I call them _Toolbox Languages - emphasize machine-readability over human-readability.

Harder-to-transpile-to languages emphasize human-readability.

I would position Lisp as a good toolbox language. Strip away the cruft and all that remains are _sexps_ (which can be stripped down to triples).  Easy, eh?

I would position Python as a poor toolbox language.  It has too much syntax that gets in the way of automation.  Especially, the indentation stuff.

It's not impossible to transpile to Python.  It's just harder than, say transpiling to Lisp.

Javascript is a reasonable Toolbox language, but Lisp is better.

[All we really need are first-class functions and everything-is-an-expression].

Markdown is a possible toolbox language, but it has the same indentation problem that Python has. (I argue that software should be build as relative, asychronous components - Markdown makes it possible to write and elide relative blocks).

HTML is an interesting possibility. It has syntax that is _worse_ than Lisp's syntax (!), but we, already, transpile to it.

# See Also
[Toolbox Languages](https://guitarvydas.github.io/2021/03/16/Toolbox-Languages.html)
[Toolbox Languages II](https://guitarvydas.github.io/2021/04/28/Toolbox-Languages-(2).html)
[References](https://guitarvydas.github.io/2021/01/14/References.html)
[Table of Contents](https://guitarvydas.github.io/2021/05/14/Table-Of-Contents.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
