FWIW, I have a *very* different view and approach to using Ohm-JS:
- I use `m4` to compose grammars *and* semantics using `m4`'s `include()` command
- I rely on JS's behaviour to help with semantics composition - you can define a `funcion` more than once, JS will use the most recent definition
- I build pipelines of translators using /bin/bash, with each stage in the pipeline getting its own "DSL" (I've got one pipeline that is 20+ stages deep) ; this could easily be done in JS using multiple invocations of Ohm - I've done this, but, I tend to gravitate towards /bin/bash ; the different DSLs are slight variations of each other, i.e. not hard to build (e.g. removing noise syntax, etc.)
- I think that mixing grammar rules together makes thinking about this stuff a lot harder (contrary to to popular belief)
- I think in layers - starting with a lexical pass to grind through character combinations, then pass "tokens" on to other passes (I build comma-less languages, where I need to insert virtual commas to keep identifiers distinct from one another, allowing space-skipping to be used in subsequent passes ; I choose some arbitrary Unicode character to be my virtual comma) ; I don't actually create tokens, but I insert doo-dads into text with more information (I don't build trees and data structures, I build text with semantic information in it, each pass adds a bit more info) ; Left-handles are friends of efficiency, inserting a character at the front of a piece of information lets the parser do less work and waste less time (I don't have concrete measurements of this fact, but have built up a gut-feel over decades of thinking this way)
- I think that the Holy Grail of FP is to write programs which can be manipulated at the text level - Ohm-JS is perfect for this kind of thing (better than most FP languages)
- I think in terms of "transpilers" - text-to-text converters ; for example, I'm currently resurrecting a Scheme to JavaScript thingie, I can let JavaScript compilers do the heavy lifting (memory allocation, instruction selection, etc) ; Odin is on my radar, too (no GC, better-than-C)
- It is a *lot* easier to tune a solution to a particular problem - "SCN" Solution Centric Notation - than to use the concept of a General Purpose programming Languages ; for example, in the above "Scheme to JavaScript transpiler thingie", I focus only on a single program - PROLOG written in Scheme - instead of trying to parse every nuance of Scheme ; it's kind of like a REGEX use-case, I write rules to grok the input program and then I write semantics to rewrite the input (e.g. PROLOG written in Scheme rewritten as JavaScript), where Ohm-JS (PEG) is *much* better for this kind of thing than REGEX, due to PEG's ability to match bookends (pairs of brackets)
- I eschew the use of `if...then...else` in my code and let Ohm-JS handle control-flow for me
- PEG is a DSL for writing parsers, PEG not a language spec (Ohm-JS is the "best" PEG-building tool I've found, especially when coupled with Ohm-editor)
- one of my goals is to build a `transpile` component and to use `draw.io` to program my pipelines (visual shell instead of /bin/bash)
- I wrote (in Ohm-JS) an SCN ("DSL") for writing semantics - `rwr` SCN for writing semantics code (formerly known as FAB, formerly known as FMT-JS, formerly known as GRASEM, etc.)

I will stop here, but, I would be happy to elucidate, contact me if you want more info.




# Appendix - See Also

### References

[https://guitarvydas.github.io/2004/01/06/References.html](https://guitarvydas.github.io/2024/01/06/References.html)

### Blog
[blog](https://guitarvydas.github.io/)

### Blog
[obsidian blogs](https://publish.obsidian.md/programmingsimplicity) (see blogs that begin with a date 202x-xx-xx-)
### Videos
[videos - programming simplicity playlist](https://www.youtube.com/@programmingsimplicity2980)
### Books (WIP)
[leanpub](https://leanpub.com/u/paul-tarvydas)
### Pamphlets
[gumroad](https://tarvydas.gumroad.com/l/dvtej?_gl=1*o7hy6z*_ga*MjA0NzUyMDY1Mi4xNzA3NDc3MDIx*_ga_6LJN6D94N6*MTcwNzQ3NzAyMC4xLjEuMTcwNzQ3NzI5Ni4wLjAuMA..)
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
