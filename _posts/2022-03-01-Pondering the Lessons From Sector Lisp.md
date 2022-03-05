---
layout: post
title:  "Pondering the Lessons From Sector Lisp"
---

bizarre observation #1: JavaScript prototype inheritance and Common Lisp specials are most similar to McCarthy's original alists

bizarre observation #2: McCarthy's Lisp is - wait for it - a DSL for List Processing.  As soon as we try to add mutation to that simple notation, we get epicycles.  By inference, Mathematics notation is a DSL for List Processing (invented for pen-and-paper).  Mathematics is 2 things: (1) a DSL, and, (2) hard-won knowledge (theorems/laws) about using that notation.

Example of simple notation:
1. x = [a]
2. x = [b|x]
3. x = [c|x]
In most GPLs, x is mutated, but in SL, x is augmented.  In SL, this is written as
- (let ((x (cons 'a nil)))
-   (let ((x-prime (cons 'b x))))
-     (let ((x-prime-prime (cons 'c x))))
-       ... do something with x-prime-prime ... 
-       (x and x-prime are shadowed by x-prime-prime ; in fact, we might call the value "x" in all cases, dropping the -prime)

mutation is an optimization - instead of keeping >1 copy of a named-value, we fold all copies into 1 ; McCarthy's Lisp keeps a (dynamic) stack of values for every name ; (mutation is structure sharing in the small?)

cycle in data is an optimization and infinite-recursion preventer

cycle is the exception, not the rule, need syntax for @cycle() instead of hard-wiring mutation into every language? ; maybe separate language that allows @cycle()? ; it is easy to create languages (using Ohm-JS/PEG)

adding mutation, adding cycles, breaking strict stack-like ordering

create a "shell" DSL that allows mutation, no need to hack on SL

---

current pondering (for discussion):

code bloat comes from conflation of (a) mutation, with, (b) the idea of "one language to rule them all"

mutation is /sometimes/ necessary, but, there is no reason to hack mutation into every existing language and to pay for epicycles everywhere

SL is a /notation/ for List Processing without mutation (=> no cycles, alists).

If/when we need mutation, we should not insert it into SL.  We can use a different /notation/.  It used to be considered "hard" to build languages, but, now it is easy to build /notations/ using PEG

remove mutation from OO, if you need mutable objects, use Actors

mutation is an optimization - structure sharing - thought to be needed in mid-1900s due to expensive CPUs and limited memory

(syn x y a) -> (let ((x y)) a) --> editor(s) can elide to just "a" and provide the synonym (syn) in a tooltip or keystroke to unelide whole buffer

need a syntax for object slots that doesn't imply operation (not car/first, second, etc.), e.g. obj=(x . (y . z)) -> (slot obj 'y) -> obj.y (again, mutation has seeped into most languages - obj is most often represented as a cdr-less array, which is just any optimization of obj from list form to cdr-less form) ; compilers should not compile data to blocks but to lists, e.g. "y" is not an offset, but a function (a list accessing function)

state for tracking history = alist (stack), optimization = mutation/overwrite
state for iterator
state for queue
state for stack pointer
StateChart
Actor

---

bizarre observation #3: The preferred way to build GUIs today is The Browser.  The API for Browsers is JavaScript.  AFAICT CLOG makes the browser a stand-alone GUI server that accepts GUI API commands and interprets them.

bizarre observation #4: In the back of my mind, I have felt that "data" should be active.  Data should be prefixed with a lump of code that executes and produces the data.  Data is an Actor.  Or, data is a lambda. BLC and SL invoke these thoughts again.

bizarre observation #5: Mutation is an optimization.  Instead of keeping a stack of values for every named "variable", we save memory by overwriting (aka optimization).

# See Also

[Table of Contents](https://guitarvydas.github.io/2021/12/10/Table-of-Contents-Dec-01-2021.html)
[Blog](https://guitarvydas.github.io)
[Videos](https://www.youtube.com/channel/UC9EJr0nKHwadbHUtc5zHdmQ/videos)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
