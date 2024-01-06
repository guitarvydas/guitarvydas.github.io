# Macros for Non-Lisp Languages
This note shows a simple technique for creating macros for textual, non-lisp, languages.

A nonsensical grammar is used.  The grammar is about 5 lines long, the transpilation semantics code is about 4 lines long.

The code repo for the working example is supplied, below.

This tool uses OhmJS and a tiny DSL that converts `.rwr` specifications into Javascript that is compatible with OhmJS requirements for semantics code.
# Nonsensical Nano-Grammar

```
hamburger {
  characters = character+
  character =
    | applySyntactic<Macro> -- macro
    | any -- other
  Macro = "I" "want" "a" "hamburger"
}
```

Input:
```
a b c I want a hamburger d e f

```

Screenshot:
![hamburger grammar](/screenshots/hamburger%20grammar%20Screenshot%202024-01-05%20at%207.25.55 AM.png)
After parsing the input, we output
```
a b c⎨
kitchen.order("hamburger");
⎬d e f
```
where "`⎨...⎬`" delimits a piece of *verbatim* code.  Downstream passes are expected to skip over *verbatim* code, since it has already been preprocessed.

The final output in this simplistic example is:
```
a b c
kitchen.order("hamburger");
d e f
```

# Explanation
The grammar is written in OhmJS syntax.

The grammar looks at every incoming character and tries to find a longest match with the macro phrase. If the phrase can't be matched, the character is left alone and output "as is".

Once the pattern matching engine finishes with a successful parse, it starts up the semantics tree-walk.  When using off-the-shelf OhmJS, the semantics are written in Javascript.  I use a tiny DSL and specify text-to-text rewriting using `.rwr` specifications instead of manually writing Javascript code.  The rewriter only rewrites strings that were matched by the "Macro" rule. The rest of the input is simply written back out "as is".

Lisp macros allow the use of macros within macros. This kind of thing comes for free with OhmJS pattern-matching, but, doesn't show up in this simple example. To get this kind of recursive pattern-matching, one needs to write grammar rules that are recursive. That kind of thing is easy, but, again, is not shown in this simple example.

We use a Lexical rule at the top level. The rule is named `characters`. The rule tells the parser to look for 1 or more instances of a sub-rule named `character`. 

In OhmJS, case is significant and meaningful. 

A rule that has a name beginning with a lower-case letter is a Lexical rule.

A rule that has a name beginning with an upper-case letter is a Syntactic rule.  Syntactic rules skip over spaces, making the rules more human-readable. Syntactic rules contain only the high-level details of the grammar, without needing to mention low-level details, like spaces.

Most PEG parsing libraries, except OhmJS, use Lexical rules that expect the grammar writer to specify every niggly detail, including where whitespace might appear.  OhmJS's Syntactic rules allow programmers to specify grammars that are more readable and easier to understand.

PEG, itself, has a power that is not found in CFG nor REGEX technology - the ability to parse matching pairs of items (usually parentheses and brackets). This simple feature makes it possible to re-think how parsers are used. For example, PEG makes it possible to write many nano-parsers and to "skip over" uninteresting bits of text, instead of specifying the full grammar for the incoming language. 

This line of reasoning leads to the idea of converting (transpiling) macros embedded in larger lumps of text, say, adding some new syntax feature to C++, or making it possible to write some Lisp code in infix form.

PEG ideas have been around for a long time, being called "recursive descent parsing".  PEG further incorporates backtracking. PEG formalizes the concept of recursive descent parsing with backtracking and makes it more accessible.

I like to think that CFGs are used for specifying *languages* whereas PEGs are used for specifying *parsers*. Their grammars look similar, but, the restrictions and effects are different.

When building a full-blown compiler, I would use a CFG and a gruelingly-detailed grammar to parse the incoming source code to catch all niggly syntax errors. A technique I've seen used is to use a strict CFG, like YACC to check the grammar for completeness and LALR-ness, then to re-express the same grammar in PEG syntax. This trick uses YACC as a linter, but, not as a code generator.

PEGs are handier and their grammars require a lot less work (minutes instead of days) when writing little transpilers for little languages. 

PEGs make it possible to use grammars in a new way, like using REGEXes, but better. PEGs can match "structured languages" whereas REGEX is designed only to match lines of text, instead of following nested structure. It is possible to kludge REGEX code into parsing across many lines, but PEGs make this more convenient and more natural.

The disadvantage of PEGs is that they require multi-line grammars and associated multi-line "semantics" (rewriting) code.  REGEX syntax is more succinct and patterns can be written in one line. Some consider REGEX patterns to be *too* succinct and unreadable, and, as already mentioned, REGEX patterns are technically limited and cannot easily parse structure.

Another "disadvantage" of PEGs is that they do not lend themselves to being used - easily and naturally - in text-based programming situations.  Expressing OhmJS (essentially a PEG) in a DPL (Diagrammatic Programming Language) makes it easier to express plugging many nano-transpilers together to form bigger transpilers.  Composing nano-transpilers by plugging them together makes it possible to use a technique called "syntax directed translation", which makes it easier to build big transpilers by narrowing one's focus down onto sub-problems (a manifestation of the "divide and conquer" technique). 

Until now, the idea of *macros* in programming languages has been restricted, mostly, to lisp-like languages. The idea of *macros* is easier to imagine and manage when the source code is converted to lists instead of remaining in text form, hence, macro-ology has been championed by Lispers.

Aside: I would argue that the epitome of *Functional Programming* is to treat all code as *macros*.  If you think about the rules for *Functional Programming*, you see that the trend is to snip all possibility of side-effects and mutation, driving towards a notation that can be manipulated like equations on paper. "Referential transparency" allows one to textually replace pieces of code with other code. The rules for *Functional Programming* are geared towards supporting referential transparency.

With PEG - and especially OhmJS coupled with the techniques in this note (bracket pairing and `applySyntactic<...>`) - it becomes possible to process macros for all text-based languages.

It is easier to process macros in separate passes instead of struggling to embed macro-processing in the language itself. You get simplicity - hygiene comes "for free". You get divide-and-conquer. In 1950s-think, it is considered wasteful to use multiple passes to do something that you can do in one pass. The trade-off is increased complexity. In 1950, it made sense to waste programmers' time and to make things more complicated in order to save storage space. In 2024, this no longer makes sense. Let a machine do the work for you. If the result is provably slow, and, can be measured as such, then go ahead and waste programmer-time by optimizing. Otherwise, leave it alone and move on to something more interesting. 

Note, also, that DPLs become instantly possible to design and implement - Diagrammatic Programming Languages. Most modern diagram editors save diagrams in some form of XML (e.g. graphML). XML is parsable text.  OhmJS parses text, hence, OhmJS can parse XML, hence, OhmJS can parse diagrams.  I show the use of this technique to create running programs elsewhere, e.g. in the code repo [0d](https://github.com/guitarvydas/0d)

## ApplySyntactic

OhmJS does a lot of type checking.  One of the things that it checks for is that Lexical rules must only invoke other Lexical rules (lower-case names, no space-skipping).  If you try to use a Syntactic rule-call inside a Lexical rule, OhmJS will signal an error. 

The `applySyntactic<...>` construct allows you to break the above check.  With `applySyntactic<...>` you can use a Syntactic rule inside a Lexical rule.

The macro-processing technique described above uses "big" rules to detect macros. The "big" rules - macros - look less noisy if they are written in Syntactic form.  So, I use `applySyntactic<...>` when defining macros, but I need to use Lexical rules at the top level, to ensure that the engine looks at every incoming character.

I like this feature, but, it is not essential to the basic technique. OTOH, I believe that human readability is paramount, and, I am willing to trade off machine time to make my grammars more readable. So, I try to write grammars using Syntactic rules as much as possible.  When I write a pattern-match for Macros, I want to use Syntactic rules, but, I need to, also, ensure that the top-most rule is Lexical.  The use of `applySyntactic<...>` makes it possible for me to mix and match rules, while letting OhmJS type check as much of the grammar code as possible.

# Further Processing
In the example code in the repo, `pass2` inhales the output from the `hamburger` pass and strips off all verbatim brackets.  We *could* mute the other characters by simply outputting nothing. In general, though, some other processing happens, in a series of further passes, such that every input phrase is ultimately rewritten. For this simple example, then, it makes little sense to show how to mute output. Doing this should be obvious to the reader, anyway, by just changing `character_other [c] = ‛«c»’` to be `character_other [c] = ‛’.

The working example is in the repo [hamburger](https://github.com/guitarvydas/hamburger)

# Omissions
I don't explain the `.rwr` syntax in this note. 

`.rwr` files are an adjunct to `.ohm` files.

`Rwr` stands for *rewrite*.  Rwr specifications are what OhmJS calls *semantics* code.  OhmJS expects semantics code to be written in Javascript.  The `.rwr` processor converts the rwr specification into Javascript suitable for use with OhmJS grammars.  Rwr deals only with strings and interpolated strings, instead of dealing with the full gamut of possibilities allowed in full-blown Javascript semantics code.  This restriction seems to be sufficient for describing a large range of transpiler applications. `Rwr` is quite succinct, too, which makes this trade-off worthwhile.

There is a 1:1 correspondence between `.ohm` rules and `.rwr` rules.  Exactly one `.rwr` rule for each `.ohm` rule.  There are some simple exceptions that allow omission of very simple rewrite rules, i.e. single-parameter semantics rules are automatically handled by the OhmJS engine (as described in the OhmJS documentation).

Rwr syntax includes experimental syntax for *pre*-treewalk code, ie. Javascript code that runs *before* a branch of semantics code is executed. This experimental syntax allows OhmJS users to set up per-rule environments that can be accessed in lower-level rules. In general, you set up stacks of environment values that act as scopes for code generation further down.

# Possibilities
In an ideal world, programmers would have access to a bag of functionality, then wrap little syntaxes (plural) around that functionality to make bits of the bag more accessible to users. 

At present, production versions of Common Lisp are the closest thing we've got to huge bags of functionality.  Common Lisp imposes very little pesky syntax of its own. It becomes possible to write little languages that output scripts of Common Lisp and lean on the (mature) Common Lisp compilers to do the rest of the work of compiling and executing and debugging.

I have successfully generated little languages that emit Common Lisp, Javascript, Python and Prolog (SWIPL) code.  Common Lisp is the "easiest" since it has a very regular syntax (if you want to call it a syntax), whereas Javascript and Python are usable, but their syntaxes make code generation just a bit more difficult.

I've also written a transpiler that converted Scheme code to Javascript to produce a usable library of code. In this particular case, I converted Nils Holm's Prolog-in-Scheme code to Javascript, producing a Prolog-like library for Javascript. Relational languages, like Prolog, have a better syntax and semantics for exhaustive search than anything else I've seen. I would imagine that miniKanren falls into this category, too, but, I haven't tried it.

I would think that "assemblers" like JVM and WASM would be easy targets for the above technique, but, again, I haven't tried to emit them.  I did generate some WASM (WABT) code, as a proof of concept, but, I didn't take it much further.

The availability of easy-to-create syntaxes brings up new ideas, like the specification of project-specific Design Rule DSLs and project-specific DSLs. This kind of thing has been done in the past, but, using REGEXs. If you use a REGEX in, say, Python, then you are actually using a DSL for pattern matching.  That DSL - REGEX - is very general. With the techniques described here, you can write code that is less general and is more project specific, e.g. you can use this stuff in place of some project-specific documentation. Documentation that can be compiled and executed is better than documentation that can't be compiled and executed.

The fact that OhmJS lets you write phrase-based DSLs without any esoteric syntax, e.g. lisp-like parentheses, makes it possible to document Design Intent in an executable manner.

Using the above techniques, it should become possible to more accurately - executably - track provenance from Architecture to Implementation.  For example, the Architecture could be expressed as a series of (transpilable) phrases. Optimizations of the Architecture could use the same starting grammar and to layer different `.rwr` files onto them, and/or, write little languages that map the original Architecture into more-optimized versions of code.

It becomes possible to use Orthogonal Programming techniques, such as those used in *gcc* and documented in Fraser/Davidson's *peephole* paper and extended by Cordy's Orthogonal Code Generator work. In essence, a code generator is split into two phases.  The first phase generates code - any code, regardless of efficiency. The second phase cleans up the code by pattern matching for idioms an replacing them with tighter code.

This, then leads, to the concept of Orthogonal Programming Languages.  Code is clearly written as two kinds of things:
1. operations
2. operands.

The programming language community already has experience with *operands*, i.e. OOP and Functions.  *Operations*, though, express *control flow*, which, with the above techniques, can be formed in human-like phrases. Assembler does this, but is limited by its line-orientation and emphasis on inexpensive parsing. OhmJS+rwr make it possible to make phrases that span multiple lines and add syntactic structure (nesting, scoping), all the while maintaining simplicity of implementation.

Almost bizarrely, Assembler already displays the use of Orthogonal programming, but in a syntactically stunted manner. In
```
MOV R0,R1
```

The text string `MOV` is an *operator*. The text strings `R0` and `R1` are operands.  

## I'm Getting Hungry
Expanding on this kind of thing, in 2024, we can easily write grammars for things like
```
I want a hamburger with bacon.crispy()and tomatoes.sliced(thin);
```
The phrase `I want a hamburger` resolves into some kind of operation. The phrase `with` is just syntactic noise. The phrases`bacon.crispy()` and `tomatoes.sliced(thin)` are operands containing method invocations. 

Let's imagine that the above turns into a line of code to be executed by the *kitchen* object, something like
```
kitchen.order(hamburger, [bacon.crispy(),tomatoes.sliced(thin)]);
```

A peepholer can post-process the resulting code and look for idioms. Let's say that the whole phrase with operands above maps into menu item #1, 
```
kitchen.order_menu_item(1);
```
the idiom 
```
kitchen.order_menu_item(1);
kitchen.order_menu_item(1);
```
is converted into something like 
```
kitchen.multiple_order(2, menu_item(1));
```
and something like
```
kitchen.order(hamburger, [cheese().bacon.crispy(),tomatoes.sliced(thin)]);
```
becomes
```
kitchen.order(cheeseburger, [bacon.crispy(),tomatoes.sliced(thin)]);
```
Prolog and its descendants make this kind of thing easy to implement. OhmJS incorporates backtracking, maybe OhmJS+RWR is enough technology for accomplishing these kinds of rewrites?

# Appendix - See Also

### References

[https://guitarvydas.github.io/2004/01/06/References.html](https://guitarvydas.github.io/2024/01/06/References.html)

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
