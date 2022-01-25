---
layout: post
title:  "Parsing for Transpilers"
---
I've grown tired of building compilers.

I have begun to use parsers for creating transpilers - source-to-source reformatters (aka bulk editing, compilation, etc.) - and leave the "hard work" to existing compilers.

I built a tool for myself that I call `prep`.  It rhymes with `grep` and has the prefix `pre` in it (that stands for "pre-processing" in my mind).

`Prep` chops up text files into blocks, then runs full-blown parsing and reformatting on the blocks.

If you use Common Lisp or Racket, you know this process by the name of `macros`[^3].

[^3]: C Macros aren't nearly as interesting as Lisp macros.

The difference is that `prep` works on characters, whereas Lisp and Racket macros deal with lists[^1].

[^1]: You *can* reformat text with Racket and Lisp, it just ain't as convenient as using `prep`.

Simplifying pattern-matching down to a simple tool like `prep` allows you to invent languages that aren't based on grids of non-overlapping cells, i.e. lines of text.

Everything that is presently done with compilers can be done with pattern matching and inferencing.

Parsers don't use inferencing because of an embargo on Early's method, based on the biases of the mid-1900's - i.e. save space and don't over-use the CPU.

Lately, inferencing has leaked back into pattern-matching, in the form of PEG parsers.

I used PEG for some work, then found Ohm-JS.  

Ohm-JS simplifies the act of creating pattern-matchers - a subtle, but, vital ingredient.

I currently use Ohm-JS for pattern matching and SWIPL for inferencing.

## Alan Kay - Use Languages as Assembly Code

*In a 'real' Computer Science, the best languages of an era should serve as 'assembly code' for the next generation of expression.*

[Alan Kay on youtube - see 31:50](https://www.youtube.com/watch?v=fhOHn9TClXY&t=859s)[^2]

[^2]: Thanks to Rajiv Abraham for sending me this clip.

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
# See Also
(*The following tools are like POCs.  They work, but are fairly new and could use some polishing*).

[PREP](https://www.youtube.com/watch?v=-I-KQjC0oBY)
[d2py](https://guitarvydas.github.io/2022/01/25/Diagram-to-Python-Transpiler.html)
[DaS Workbench](https://guitarvydas.github.io/2021/07/30/Parsing-Diagrams-DaS-Workbench-Overview.html)

[References](https://guitarvydas.github.io/2021/01/14/References.html)
[Table of Contents](https://guitarvydas.github.io/2021/12/10/Table-of-Contents-Dec-01-2021.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
