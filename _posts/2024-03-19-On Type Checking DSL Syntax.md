I would prefer to see code like this:
```
function fn (i, f) {
    r = i + f
    return r
}
```

instead of the overly-busy syntax that we see today:
```
function fn (i : i8, f : f64) -> f64 {
    var r : f64
    r = (cast (f64) i) + f
    return r
}
```

# Thoughts...
We might augment the first lump of code with a separate text section that is written specifically for the type-checker DSL:
```
fn   = (i8, f64) -> f64
fn/i = i8
fn/f = f64
fn/r = fn/f
fn/+ = (cast(fn/f, fn/i), fn/f) -> f64
```

The type checker could simply ignore the first lump of code and deal explicitly with the *types* section, instead of tangling everything together and making it all look magical and complicated and busy.

Here, in the type DSL, names are *not* variables, they are *types*. For example, `fn/f` is not the runtime variable `f`. `fn/f`  is a *type* within the scope of `fn`, which is intimately related to the runtime variable `f`. 

Basically, the idea is to strip out the type-checker DSL from the Design Engineering DSL and make explicit the fact that the type-checker is a separate entity and that the type-checker DSL is *only* there to help Production Engineering developers, since End-Users, Architects, Design Engineers, GUI Engineers, Security Engineers, Test Engineers, etc. don't really care about these kinds of details.

The type-checker-DSL allows types to be defined in terms of other types, with only a few basic built-in types, like i8, f64, etc., at the lowest, bottom level.

The *cast* operator is a type operation which *might* add runtime code to stretch one of the operands into alignment (in this example, the first operand of fn/+).  Unanswered question: does *cast* belong in the type-DSL exclusively? Observation: in the Odin programming language, *"cast"* is a code-generating operation, whereas *"transmute"* is a purely type-checking operation that never produces any code. Is *cast* two different things in the above? Is it (1) a type operation, *and* (2) an allocator / code-inserter operation? Does this suggest yet another DSL - for the allocator? As a compiler writer steeped in syntax-directed translation, I would say "yes", and, I would say that the first syntax is targeted at humans, whereas all of the rest of the stuff is meant only for detail-oriented humans, e.g. Production Engineers, who can use automated tools, like type inferencers, to help them do their work, whilst maintaining provenance with respect to the original DI (Design Intent). To build such automated tools, it helps to build machine-oriented syntaxes and to use syntax-directed translation, i.e. not all syntaxes must be designed to be human-readable, it is beneficial to design syntaxes that support machine-readability and easy manipulation by relatively "dumb" machines.

Fundamentally, the Design Engineer doesn't want to worry about such niggly details, but, the Production Engineer does need to worry about them. Schmooing all concerns into a single language just makes things look more complicated than is necessary and tends to water down one, or more, of the concerns.

# Scoping in Type DSLs
If you think about a DSL meant only for types, you might want to add scoping of type names to reduce noise in the type language. For example:
```
fn = (i8, f64) -> f64
in scope of fn {
  i = i8
  f = f64
  r = f
  + = (cast(f, i), f) -> f64
}
```

# Generic Typing
Design Engineers might wish to include *some* types in their designs, while leaving out the low-level details.

Maybe, Design Engineers might want to say something like:
```
fn   = ($1, $2) -> $2
in scope of fn {
  i = $1
  f = $2
  r = f
  + = (cast(f, i), f) -> $2
}
```
# Gradual Typing
Design Engineers might wish to include *some* types in their designs, while leaving out mid-level and low-level details.

Maybe, Design Engineers might want to say something like:
```
fn   = (_, _) -> _
```
The rest of the details remain unspecified, which means that all variables are of some ultra-generic type.

This specification only says that `fn` is a subroutine that takes two arguments and returns a single value. Design Engineers could even leave that out, meaning that nothing gets type-checked and the design is essentially typeless. Note that *typeless* is not the same as *dynamically typed*. *Dynamic typing* means that type checking is, indeed, performed, but, only at runtime. *Typeless* means that no type checking is performed whatsoever, like in *assembler*.

Further refinements to the types of an application can be provided by Production Engineers, et al, using more gradual typing incrementally applied through further uses of the Type-Checking DSLs, the Allocation DSLs, etc.

An application is fully typed when all types resolve - transitively - into any of the built-in types. An application is fully typed with respect to a target CPU architecture when all types resolve into any of the built-in types directly supported by that architecture. 

# Type and Allocation Resolution
Cordy, in his thesis on Orthogonal Code Generation, built a declarative decision-tree-walking DSL, called "MIST", that would specialize code sequences based on target architectures. Cordy's work was aimed at choosing assembler instruction sequences, but, I would imagine that this same strategy would work for resolving type systems with respect to target architectures.

# Appendix - Orthogonal Code Generation
Cordy's thesis is concerned mainly with assembler code generation, yet, the technique used - especially the MIST decision tree-walking language - could be applied to checking resolved types against a declarative menu of supported types for a target architecture.

[OCG](https://books.google.ca/books?id=X0OaMQEACAAJ&dq=bibliogroup:%22University+of+Toronto+Computer+Systems+Research+Institute+Technical+Report+CSRI%22&hl=en&sa=X&ved=2ahUKEwig1Legm8bqAhWvlHIEHYzzBYEQ6AEwBHoECAEQAQs)

One of the main tenets of OCG, is the idea that data and control flow should be treated in an orthogonal manner. The MIST DSL is applied in the second - data oriented - pass of OCG.

For example, in extending this technology to type checking, in many computer languages, the operation of adding two `int`s can result in overflow, hence, the operation must be cast to a wider result type if no precision is to be lost. A thorough type checker must ensure that the runtime code does such casting. If the source programming language requires programmers to specify all types, as in Odin, then an error must be generated in cases where the appropriate cast is not specified, whereas in languages that provide auto-casting, extra code might need to be generated. These kinds of type-checking decisions are often performed using ad-hoc code. Cordy shows how to collapse such decision trees into a small DSL designed expressly for the purpose.

A precursor to OCG is used in the GCC compiler. This precursor is `RTL`, described in [Peephole optimizer](https://www.researchgate.net/publication/220404697_The_Design_and_Application_of_a_Retargetable_Peephole_Optimizer). The idea here, again, is data and control flow orthogonality. On the first pass, an RTL compiler generates code for a fictitious machine that has an infinite number of registers. The second pass uses a simple pattern-matching algorithm that uses a window to detect boiler-plate usage patterns and replaces such code sequences with different ("better") sequences of code using various heuristics based on the instruction and allocation realities of a specific target. This strategy produces code which is locally optimized. GCC then goes on to use global optimization techniques, such as those described in the *Dragon Book* to produce even tighter code sequences. 
# Appendix - See Also

### References

[references](https://guitarvydas.github.io/2024/01/06/References.html)

### Blog
[blog](https://guitarvydas.github.io/)

### Blog
[obsidian blogs](https://publish.obsidian.md/programmingsimplicity) (see blogs that begin with a date 202x-xx-xx-)
### Videos
[videos - programming simplicity playlist](https://www.youtube.com/@programmingsimplicity2980)
### Books (WIP)
[leanpub](https://leanpub.com/u/paul-tarvydas)
### Pamphlets
[A DSL For Writing DSLs](https://tarvydas.gumroad.com/l/hiypq?_gl=1*1kki8v2*_ga*NTI5MDkzNTI0LjE3MTAzNTQzNjU.*_ga_6LJN6D94N6*MTcxMDg2NDAyNy41LjEuMTcxMDg2NDAyOC4wLjAuMA..)
[Wond'ring Aloud: Is Concurrency Difficult?](https://tarvydas.gumroad.com/l/dvtej?_gl=1*o7hy6z*_ga*MjA0NzUyMDY1Mi4xNzA3NDc3MDIx*_ga_6LJN6D94N6*MTcwNzQ3NzAyMC4xLjEuMTcwNzQ3NzI5Ni4wLjAuMA..)
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
