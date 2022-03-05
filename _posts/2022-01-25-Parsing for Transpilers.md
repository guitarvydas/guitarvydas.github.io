---
layout: post
title:  "Parsing for Transpilers"
---
I've grown tired of building compilers.

I have begun to use parsers for creating transpilers - source-to-source reformatters (aka bulk editing, compilation, etc.) - leaving the "hard work" to existing compilers.

I built a tool for myself that I call `prep`.  It rhymes with `grep` and has the prefix `pre` in it (that stands for "pre-processing" in my mind).

`Prep` chops up text files into blocks, then runs full-blown parsing and reformatting on the blocks.

If you use Common Lisp or Racket, you know this process by the name of `macros`[^3].

[^3]: C Macros aren't nearly as interesting as Lisp macros.

The difference is that `prep` works on characters, whereas Lisp and Racket macros deal with lists[^1].

[^1]: You *can* reformat text with Racket and Lisp, it just ain't as convenient as using `prep`.

Boiling pattern-matching down to an easy-to-use tool frees one to invent languages that aren't based on grids of non-overlapping bitmaps, i.e. lines of text.

Everything that is presently done with compilers can be done with pattern matching and inferencing.

Parsers don't use inferencing because of an embargo on Early's method, based on the biases of the mid-1900's - i.e. save space and don't over-use the CPU.

Lately, inferencing has leaked back into the parsing world, in the form of PEG parsers.

I used PEG at first, then found Ohm-JS.  

Ohm-JS simplifies the act of creating pattern-matchers - a subtle, but, vital aspect for development.  For example, LR(k) and LL(k) parsers make one "think compilers", and PEG, while freer, still feels like a compiler technology.

REGEX broke free of compilerdom and enabled a new class of languages and thought patterns[^2].

[^2]: Like *perl* and *grep* and regular expressions in Python and JavaScript.

I believe that Ohm-JS can enable new thought patterns, even better than those enabled by REGEX.

I currently use Ohm-JS for pattern matching and SWIPL for inferencing.

## Alan Kay - Use Languages as Assembly Code

*In a 'real' Computer Science, the best languages of an era should serve as 'assembly code' for the next generation of expression.*

[Alan Kay on youtube - see 31:50](https://www.youtube.com/watch?v=fhOHn9TClXY&t=859s)[^2]


[^2]: Thanks to Rajiv Abraham for sending me this clip.

Layering syntax over top of existing languages using Ohm is one way to accomplish this kind of expressiveness.

Thinking this way has led me into down into new rabbit holes, e.g.
- I conclude that syntax is frivolous, paradigms are essential,
- I want toolbox languages that help me write code that writes code,
- I conclude that we need to deprecate all programming languages and operating systems[^1].
 
[^1]: 11th Rule: Programming Languages are IDE wannabes.

## Pipelines
I use `prep` in pipelines - not just one parser, but a series of parsers.

I happen to use UNIX® pipelines, but pipelining can be easily done in HTML with a sprinkling of JavaScript (see the daswb POC).
## Diagrams to Python
An example of transpiling can be seen in the `d2py` code.

The diagram, `helloworld.drawio` is 
- transpiled into PROLOG
- then inferenced
- then transpiled into JSON
- then transpiled into Python.
## See Also
(*The following tools are like POCs.  They work, but are fairly new and could use some polishing*).

[PREP](https://www.youtube.com/watch?v=-I-KQjC0oBY)
[d2py](https://guitarvydas.github.io/2022/01/25/Diagram-to-Python-Transpiler.html)
[DaS Workbench](https://guitarvydas.github.io/2021/07/30/Parsing-Diagrams-DaS-Workbench-Overview.html)

[Ohm-jS](https://github.com/harc/ohm)
[SWIPL](https://www.swi-prolog.org)

# See Also

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
