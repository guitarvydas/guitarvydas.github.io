2024-06-12-Smallness

# Keep Types Simple

e.g. index:

* \> 0 ≡ Atom
* \< 0 ≡ Cons cell
* = 0 ≡ Nil

The above types are fundamentally supported by most CPUs. Branch on 0, branch on positive, branch on negative. *From: McCarthy’s Lisp 1.5 and Sector Lisp.*

# Pure FP

Functional Programming (FP) means that data is *always* allocated on a stack. This means that GC (Garbage Collection) can be greatly simplified.  For example Cons cells can only be generated in a stack-like manner by a function. Reset the Cons cell stack pointer when the function terminates, keep only the cells that need to be returned from the function. Sector Lisp uses the ABC garbage collection algorithm, which works atomically with the cells on the stack starting at the stack pointer when the function was entered. ABC has a pointer to the cell that needs to be returned. All other cells can be reclaimed by moving the kept cell down in the stack to the previous position of the stack pointer, eg.

*Diagram should display here:*

![](/assets/ABCGC.png)

*Diagram should, also, display here:*
![][ABCGC]

# Interning

All atoms are created only once. The algorithm is:

Read an Atom from the text input (e.g. a keyword) and convert it into internal form as follows:

* Check if the Atom already exists in memory, return its pointer
* If the Atom does not exist, create a new slot for it in memory and return a pointer to that.

This is essentially a hash-table strategy. McCarthy did not use hash tables and did a linear search through Atom space. We can do better, now.



[ABCGC]: /assets/ABCGC.png width=325px height=181px
