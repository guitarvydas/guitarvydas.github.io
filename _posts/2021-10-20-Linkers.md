---
layout: post
title:  "Linkers"
---
# Synopsis
You always use a linker, but its use is usually hidden from you.

# Appendix
If you use any code library, the system uses a linker.

Most languages use a "runtime library" to do the work that is punted by the compiler. 

In this case, a linker is used.

Corollary: you would have to work very hard to *not* use a linker (library).

If you use *any* library (say, by specifying require () statements or by using a compiler that punts work to a small library), then it is likely that you will end up using a linker.

# Appendix More:
The O/S (Operating System) "helps" you by hiding certain repetitive details.

Before an app can run, the O/S must "load" it.

The O/S loads an app by bringing it into memory and then bringing into memory *all* of its dependencies (libraries).

If virtual memory is involved, the O/S does even more work.  It needs to screw around with virtual memory issues like MMUs and trying not to page in code that is "on deck" but not yet needed. 

All of this merely code, not magic.

Most modern libraries come pre-packaged with holes in them. 

The linker (loader) fills in the holes and ties the library back to app code.

# Appendix More More: 
You are *always* compiling to a low level.

Every HLL (e.g. Haskell, Python, JS, etc, et) produces low level code for you (i.e. assembler and machine code).

Then, the O/S loads that low level code and loads whatever libraries the compiled code references.

Unlike package managers, the O/S doesn't know which dependencies you need.  The dependencies must be explicitly specified (again, this is often hidden from you).

# Appendix More More More
The API to the hardware is the set of opcodes (assembler). 

All apps must boil down to that same set of opcodes. 

For example, Haskell must boil down to the same set of opcodes that C boils down to.

Haskell includes a type interpreter that C doesn't include. 

In the end, both, Haskell and C, boil down to the same set of opcodes. 

You *could* write all Haskell programs in assembler, but you don't. 

The difference is purely psychological - if you don't have to worry about *xyz*, then your imagination can soar to new heights and solve bigger problems.

# Appendix More More More More: 
The low-level CPU API is invented by chip designers. 

Chip designers work with asynchronous electronic circuits, composed as various forms of rust - oxides - created by exposing sand to various high temperatures. [Jeri Homebrew Transistor](https://www.youtube.com/watch?v=w_znRopGtbE). 

The low-level API has been debated - von Neumann architectures, Harvard architectures, RISC architectures, etc.

All of that opcode stuff is malleable and we keep asking the question of "what is the best arrangement?". 

(The answer, IMO, is that there is no ONE best arrangement. We need multiple arrangements.)

# See Also
[Jeri Homebrew Transistor](https://www.youtube.com/watch?v=w_znRopGtbE)
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
