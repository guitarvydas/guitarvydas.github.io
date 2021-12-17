---
layout: post
title:  "Access Control Privileges for Functions"
---

# Privileges for Functions
At present, access control (privileges) are used only at the operating system and server levels.

Access control makes sense at the program level.

Certain functions should only be called during certain situations.

Certain functions should only be called by privileged functions.

# Example
## Dispatcher
A Software Component might support a `react` method, but, 
- that method must only be called by the Dispatcher, and must not be called by other Software Components
- that method must only be called when the system is in `steady state`.
# AOP - Aspect Oriented Programming - Conundrum
AOP was, probably, designed to handle such cases, as the above.

Yet, AOP does not describe this specific problem.  

AOP is too general.

The conundrum, here, is that the Dispatcher example is very specific to the problem-at-hand.

The solution *can* be described using AOP, but AOP does not *enforce* that the solution be described in this way.

In fact, the solution *can* be described in assembler.  

AOP is like an assembler for multiple views on a problem.

Assembler needed to be *structured*.  Likewise, AOP needs to be *structured*.

AOP is not common in popular languages.

# OOP Conundrum
OO Programming suffers from the same sort of problem as described in the above AOP section.

OO describes one aspect of a problem, but must be contorted to cover the various situations in a given problem.

At first, popular OOP had single inheritance.  That wasn't enough, so multiple inheritance was invented.  Then, mixins were invented. And interfaces were invented.

Each invention was good for specific use-cases, but none was general enough to cover all use-cases.

I argue that there cannot be a *one-language-to-rule-them-all*.  We need *many* notations which can be blended together to form a viable solution.

It is possible to describe a solution using only one notation, e.g. an elaborate type system, but such effort results in accidental complexity and wasted design time.

# Access Control
In fact, it might turn out that access control is not appropriate for every use-case.

The use-case(s) depends on the problem-at-hand.

# Appendix - See Also
[Blog](https://guitarvydas.github.io)
[Table of Contents as of Dec. 01, 2021](https://guitarvydas.github.io/2021/12/01/Table-of-Contents-December-01-2021.html)
[Videos](https://www.youtube.com/channel/UC2bdO9l84VWGlRdeNy5)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
