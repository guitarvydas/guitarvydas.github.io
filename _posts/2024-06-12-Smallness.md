Title: 2024-06-12-Smallness  
Author: pt

2024-06-12-Smallness

# Keep Types Simple

e.g. index:

* \> 0 ≡ Atom
* \< 0 ≡ Cons cell
* = 0 ≡ Nil

The above types are fundamentally supported by most CPUs. Branch on 0, branch on positive, branch on negative. *From: McCarthy’s Lisp 1.5 and Sector Lisp.*

# Pure FP

Functional Programming (FP) means that data is *always* allocated on a stack. This means that GC (Garbage Collection) can be greatly simplified.  For example Cons cells can only be generated in a stack-like manner by a function. Reset the Cons cell stack pointer when the function terminates, keep only the cells that need to be returned from the function. Sector Lisp uses the ABC garbage collection algorithm, which works atomically with the cells on the stack starting at the stack pointer when the function was entered. ABC has a pointer to the cell that needs to be returned. All other cells can be reclaimed by moving the kept cell down in the stack to the previous position of the stack pointer, eg.

![][ABCGC]

# Interning

All atoms are created only once. The algorithm is:

Read an Atom from the text input (e.g. a keyword) and convert it into internal form as follows:

* Check if the Atom already exists in memory, return its pointer
* If the Atom does not exist, create a new slot for it in memory and return a pointer to that.

This is essentially a hash-table strategy. McCarthy did not use hash tables and did a linear search through Atom space. We can do better, now.

# Appendix - See Also

\[References\](https://guitarvydas.github.io/2024/01/06/References.html)

\[blog\](https://guitarvydas.github.io/)

\[obsidian blogs\](https://publish.obsidian.md/programmingsimplicity) (see blogs that begin with a date 202x-xx-xx-)

\[videos - programming simplicity playlist\](https://www.youtube.com/@programmingsimplicity2980)

\[leanpub\](https://leanpub.com/u/paul-tarvydas)

\[gumroad\](https://tarvydas.gumroad.com/l/dvtej?\_gl=1\*o7hy6z\*\_ga\*MjA0NzUyMDY1Mi4xNzA3NDc3MDIx\*\_ga\_6LJN6D94N6\*MTcwNzQ3NzAyMC4xLjEuMTcwNzQ3NzI5Ni4wLjAuMA..)

\[Discord: Programming Simplicity\](https://discord.gg/Jjx62ypR) all welcome, I invite more discussion of these topics, esp. regarding Drawware and 0D

Twitter: @paul\_tarvydas

<script src="https://utteranc.es/client.js" 

repo="guitarvydas/guitarvydas.github.io" 

issue-term="pathname" 

theme="github-light" 

crossorigin="anonymous" 

async> 

</script> 


[ABCGC]: ABCGC.png width=325px height=181px
