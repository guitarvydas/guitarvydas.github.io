---
layout: post
title:  "Waterfall Takeaways"
---

# Happy Path
Tha Happy Path is the path through code when "everything goes right".

# Other Paths
Software must deal with other paths through code - paths to execute when something fails.

Other paths are even more important in distributed code, e.g. internet. 

Connections might fail.

Connections might time out due to other reasons, e.g. taking too long to respond.

# Second Class Citizens

Most current PLs make it easy to write code for the happy path.

Most current PLs address code for other paths as second class issues, e.g. by providing syntactical warts, like exceptions.

# Waterfall Thinking

Thinking and coding _only_ for the happy path is Waterfall Design.

# StateCharts

StateCharts address, both, happy paths and other paths in the same way, using the same programming syntax and contstructs.

# Functions

Functions are a notation that is unbalanced.

With functions, the happy Path is first-class, and other paths are second class.

Functions address only the happy path - input, process, return a value. 

Exceptions use a different syntax and follow a different dynamic call chain for the happy path.

# Send ()

`Send ()` does not differentiate between happy path and other paths.

The syntax is the same for happy path and other paths.

The Architect can design code for multiple paths without resorting to syntactic ornaments.

# Drakon
[Drakon](http://drakon-editor.sourceforge.net/) treats other paths as first class citizens.

The Drakon tutorials are very good introductions to happy+other path notation:
- [Part 1](https://drakonhub.com/files/drakon_part1_eng.pdf)
- [Part 2](https://drakonhub.com/files/drakon_part2_eng.pdf)
- [Part 3](https://drakonhub.com/files/drakon_part3_eng.pdf)

I favor `Component Based Programming` and consider Drakon to be a subset of CBP (Drakon would be a good way to implement leaf components).

# Concurrency
It is difficult to implement other paths using synchronous, non-concurrent, code.

It is easy to implement other paths (and the happy path) in the concurrent paradigm. 

Aynchronous code and parallel code are easier to design in the concurrent paradigm.

Most current PLs treat asynchrony as a second class paradigm.

# Tell: Backtraces

Backtraces are a _tell_ that indicates happy-path-only thinking.

Happy-path-only => Waterfall design.

# Tell: Poor Error Messages

Poor error messages are a _tell_ that happy-path-only thinking has been used in the design, e.g. error handling is avoided and relegated to second class status.

Elm claims to have good error messages.

Compiler technologies researched error handling in the 1970's. (At the least, maybe earlier).

For example, you do not expect a compiler to give multiple-line warnings, multiple-line error messages and to stop after the first error.  

C gave reasonable error messages.  SBCL does not give reasonable error messages. JavaScript avoids the issue of errors and simply doesn't check for many classes of problems.

Early Lisps included experimental constructs for handling warnings and errors, e.g. restarts.  (Lisp suffered a dimunition of such abilities when CL was standardized, compilatility was emphasized over other path coding).

# FP - Functional Programming

Using FP, one is encouraged to deal with the happy path and to relegate other paths - exceptions and errors - to second class status.

(This is not surprising, since FP is based on functions, see above).


# See Also

[CALL/RETURN Spaghetti](https://guitarvydas.github.io/2020/12/09/CALL-RETURN-Spaghetti.html)
[References](https://guitarvydas.github.io/2021/01/14/References.html)
[Table of Contents](https://guitarvydas.github.io/2021/05/14/Table-Of-Contents.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
