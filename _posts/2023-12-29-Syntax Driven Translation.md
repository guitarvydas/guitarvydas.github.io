My advice: Divide and Conquer.  Use the Parser ONLY to grok whether the incoming source code is valid, checking ONLY that the source contains "tokens" in a valid sequence.  

If the parser OK's the input, the Semantic Analysis phase can figure out what each thing means.  In fact, Semantic Analysis consists of two distinct phases itself
1. collect up all declarations and make entries in some sort of "symbol table" (a map of {name X class-for-storing-info-about-each-entity}) and 
2. check that each entity is used in a valid manner.  

Pass (1) ignores anything that isn't a declaration.  Pass (2) ignores all declarations. Think in terms of an "interpreter" - i.e. what code do you need to write for each operator to check that the operands are valid.  The checking code gets to use the "symbol table" created in (1).  

"Ignoring" bits of source code is easy with OhmJS (PEG), but, is a lot harder in classical CFG approaches (like YACC).

Symbol tables are easy to make in Javascript. Create a "map" that uses a string (name) as the key and an object (class-thingie) that describes the named object.

A "compiler" is just an "interpreter" that pre-filters operations so that you don't need to do the checking at runtime.  

After Parsing, use Divide and Conquer again. Use the results of the Semantic Analysis to figure out how/where to Allocate each bit of data (i.e. stack, heap ; "scope").  After that use Divide and Conquer again to figure out what code to emit.  The Emission can be done in two phases, too, 
1. dumb emission
2. peepholing - looking for idioms and replacing them with tighter code. GCC does that using something called RTL.  

Note that you can call OhmJS more than once in a language pipeline, once for each pass above.  Compilation is easy and straight-forward, but, there's just a LOT of work to do.  You can blow your own feet off if you try to do too much in one gulp. That's also called "premature optimization".  Concentrate on only one aspect at a time.  OhmJS make this kind of thing a LOT easier, since you can just call Ohm more than once - you don't have to do everything at once.

Parse -> Semantic Gathering -> Semantic Checking -> Allocation -> Emission

Parse is written in OhmJS.  The rest in JavaScript.  

Or, you can do all of it in OhmJS.  The phases are arranged in a pipeline, each eating source code which has been modified by the previous phase. Each phase modifies the source code by culling it or inserting bits of info or by creating a separate "symbol table" (a JS map).  Each phase accepts a slightly different "source language" - machine readable, but, not necessarily human readable.  

[This approach is called "syntax driven translation".  This is the epitome of FP, a pipeline of text manipulators].

The classic approach is to think that there is only ONE source code syntax and to hang ALL work off of that syntax, i.e. conflating issues and doing anti-divide-and-conquer and allowing yourself to blow your own feet off. The "syntax driven translation" approach assumes that there are a zillion little syntaxes, where most of them are machine-readable, but, not very human-readable.  Only the very first syntax is human-readable, the rest of the intermediate, mini-syntaxes are tuned for each task.  

The ultra-FP approach is like translation-driven translation, where a symbol table is created and passed in as a parameter to each pass, or, the symbol table is effectively replaced by source-code annotations. Each pass "parses" a slightly different source code syntax.

Syntax-driven-translation needs to use a zillion little parsers.  With CFG techniques, this is hard to do. With OhmJS (PEG) techniques, this is easy to do.

I know of only one serious compiler project - PT Pascal in S/SL - that was done this way. It uses pre-PEG technology and pre-OO technology and is, therefore, harder to comprehend than necessary.

In summary, create a bunch of little grammars:
1. Use Ohm-editor to whip up a grammar that parses the main syntax
2. Use Ohm-editor to concentrate on gathering up declaration information, maybe into a JS map, or as annotations / markups of the original source code, strip out all declarations from the original source code. After gathering the info from declaration syntax, the declaration syntax becomes useless noise.
3. Use Ohm-editor to concentrate on using the gathered declaration information to check that things are being used in an acceptable manner, this is kind of like a *lint* pass.
4. Use Ohm-editor to use the gathered information to figure out where each thing should be stored ("scoping") and add that info to the symbol table, or, add more annotations to the evolving source code.
5. Reformat the already-checked and already-scoped-and-allocated code into some existing language, like JS or Python or something.
6. Finish - let the existing compiler do the rest of the heavy lifting, such as creating an executable or WASM or whatever.

# Said in a different way 
`"a + b"` is a legal syntactic phrase. The parser determines that. A subsequent phase(s) does the semantic checking. Semantically, the syntactic phrase only makes sense if `(typeof(a), typeof(b))` is a valid combination for the operator `"+"`, but, you don't build that check into the first-pass parser. How do you store and pattern match such legal combinations? I guess that I was making suggestions. At least one that I left out is: a big wad of conditional code, like 
```
if (a is an int) and (b is an int) 
  then OK
  else if (a is an int) and (b is a float) 
    then OK
    else if ... 
      else NOT_OK`. 
```
The big-wad-of-code technique only works (but is usually bug-ridden) if the overloading rules are cast in stone. If you allow the programmer to define overloaded procedures, you need to keep the overload information in some sort of dynamically-generated form, e.g. a symbol table. I guess that you could code up the big-wad-of-code idea as an OhmJS grammar (as long as the rules are cast in stone and you embellish the variables with "data descriptors"). OhmJS's backtracking is a better way of pattern matching than writing big long if-then-else's. For example, you could write a second-pass grammar that annotates the code as `⦑a,int⦒ + ⦑b,int⦒` (those are Unicode brackets), then, write a third pass grammar that checks for valid combinations. OTOH, it might be more straight-forward to do that in Javascript using a map that contains lists of valid combos. I like the annotation idea, since I believe that that is where "Functional Programming" is ultimately headed...
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
