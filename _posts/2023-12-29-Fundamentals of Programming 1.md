- don't embed knowledge of data shape in code
- don't embed knowledge of other functions in code
- inhale, then exhale
- Don't Repeat Yourself ("DRY")

# Avoiding Embedding of Data Shape in Code
OOP

The caller does not know how the data is structured.

The caller can only call methods on the data.

The methods are localized, locality of reference.  All methods that understand the shape of the data are closely associated with the data itself, and, are not sprayed throughout the code.

The methods - and *only* the methods know how the data is structured.

The caller only knows how to invoke methods, and, cannot rely on knowledge of the data structure.

# Avoiding Embedding Knowledge of Other Functions in Code
- indirection
- not implicitly supported by popular programming languages
	- most PLs allows calling functions by name, which hard-wires knowledge of the target functions into the caller's code, which sprays coupling throughout the code base
- most PLs support function *input* parameters, but, do not support function *output* parameters
- DLLs were invented to work around this kind of problem, yet, still couple callers and callees via the callstack.  The callee *must* return to the *caller* because of the callstack protocol.  This is a form of coupling.

# Inhale, Then Exhale
Inhaling consists of grokking the input source.  Often this is called "parsing", or, "input validation".

Use exhaustive search to grok the input. E.g. Prolog, or miniKanren, or ...

Exhaling consists of reformatting the inhaled source and outputting the result.

There is no good reason to use the *same* technologies for, both, inhaling and exhaling.  For example, you might use a *parser* (my current favourite is OhmJS) to parse the input, but you don't need to use it to create output.  Javascript *template strings* and Python *formatted strings* are good enough for this task.  Use both technologies, not just a single one.  The problem is compounded if you enhance the inhalation process by using Prolog.  It is *possible* to use Prolog to format output, but Javascript is is more convenient.

# Don't Repeat Yourself
This is a *secret* of good programming that is learned in University by osmosis.

It is better to have only *one* copy of any code or any data structure.  This is "locality of reference".  If you want to make a change, you should make the change in only one place. If you have to edit more than one piece of code, you will inevitably forget to make the change somewhere. This leads to mysterious bugs and long debugging sessions.

Techniques for DRY consist of *abstraction* and *parameterization*.  We pull out the common bits of code and create a single subroutine containing the common aspects.  After a while, the common code becomes so abstract as to defy understanding. Common programming language designers throw up their hands and assume that *abstraction* is the *only* way to achieve DRY.  This approach tends towards making code unreadable.

Another approach, not taught in universities, is to snip all dependencies between code modules and to make all modules communicate via a strictly defined, very simple, protocol.  This approach localizes all code manipulation into small, self-contained units. This approach makes it possible to use RY (Repeat Yourself), but, localizes the code into self-contained black boxes. Once a box works correctly, it remains working correctly. Units can be plugged together, and instantiated, to form programs. If a change needs to be made, it is made to the innards of one black box and that black box is re-instantiated by all code that uses it.

For this approach to work, *all* dependencies, including hidden dependencies, must be removed, making each unit be truly self-contained.

This approach needs to deal with the dimension of *time*. Inputs can be sent to any unit in any order at any time. The units can produced outputs in any order and at any time.  For example, a unit might receive one parameter, then later, another parameter.  Specifying the unit as `f(x,y)` is not sufficient.  `x` might be sent to `f` before `y`, or `y` might be sent before `x`.  The notation `f(x,y)` implies that both parameters `(x,y)` are sent at the same time, instead of - maybe - at separate times in a different order.

One way to deal with the dimension of *time* is to make little envelopes that contain the data, i.e. *messages*, and, to keep ordered queues of such envelopes.  A function `f` is invoked with no parameters, then, sometime later, its parameters arrive.  Likewise, `f` can produce output parameters at any time and in any order, or, `f` can produce no output at all.  `f` can send its outputs anywhere it wants to - it is not constrained to sending the outputs back to the caller. In fact, if `f` is properly isolated, it must send its outputs to its own output queue, without knowing where such outputs will be delivered. `f`'s *Container* (its parent) makes all routing decisions. When the *Container* is properly isolated - and adheres to locality-of-reference rules - it is constrained to routing messages only between its direct children, or, back out to its own output queue, while not knowing where such outputs will be routed by its own *Container*.


# Appendix - See Also

### References

[https://guitarvydas.github.io/2021/12/15/References.html](https://guitarvydas.github.io/2021/12/15/References.html)

### Blogs
[blog](https://guitarvydas.github.io/)

[obsidian blogs](https://publish.obsidian.md/programmingsimplicity) (see blogs that begin with a date 202x-xx-xx-)
### Videos
[videos - programming simplicity playlist](https://www.youtube.com/@programmingsimplicity2980)
### Books
leanpub'ed (disclaimer: leanpub encourages publishing books before they are finalized - these books are WIPs)
[Programming Simplicity Takeaways, and, Programming Simplicity Broad Brush](https://leanpub.com/u/paul-tarvydas)
### Discord
[Programming Simplicity](https://discord.gg/Jjx62ypR) all welcome, I invite more discussion of these topics, esp. regarding Drawware and 0D
### Twitter
@paul_tarvydas
### Mastodon
(tbd, advice needed re. most appropriate server(s))

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
