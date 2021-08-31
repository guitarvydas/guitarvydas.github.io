---
layout: post
title:  "Ohm-JS"
---
[_Various musings, some half-baked, about Ohm-JS and PEG..._]

IMO, the best way to start with Ohm-JS is by using the Ohm Editor.

I wrote a small intro to the Ohm Editor, and, I wrote down my train-of-thoughts as I learned Ohm-JS (I chose to transpile a Scheme library to JS to get a js-prolog).

[Ohm Editor](https://guitarvydas.github.io/2021/05/09/Ohm-Editor.html)
[Ohm In Small Steps](https://guitarvydas.github.io/2020/12/09/OhmInSmallSteps.html)

I wrote these a long time ago and my writing style has changed (I hope that it has become "simpler").

IMO, the best way to develop a language is:
1) create the grammar with the Ohm-Editor
1a) Test the grammar using the Ohm-Editor and various language snippets.
2) Write an identity transform (input->parser->output, same output as input).
3) Modify the identity transform to suit your needs.

I modified the sample Ohm grammar (Arithmetic) to create transpilers for WASM, Python, JS and Lisp:

[WASM Prototype](https://guitarvydas.github.io/2021/05/15/WASM-Arithmetic-Transpiler.html)

[Python, JS, Lisp Prototypes](https://guitarvydas.github.io/2021/05/11/Ohm-Arithmetic.html)


Other stuff, maybe of interest:

[PEG Cheat Sheet](https://guitarvydas.github.io/2021/04/02/PEG-Cheat-Sheet.html)
[REGEX vs PEG](https://guitarvydas.github.io/2021/03/24/REGEX-vs-PEG.html)
[Racket PEG](https://guitarvydas.github.io/2021/03/19/Racket-PEG.html)
[PEG vs Other Pattern Matchers](https://guitarvydas.github.io/2021/03/17/PEG-vs.-Other-Pattern-Matchers.html)
[PEG](https://guitarvydas.github.io/2020/12/27/PEG.html)
[What If Making A Compiler Was Easy?](https://guitarvydas.github.io/2021/04/26/What-If-Making-A-Compiler-Was-Easy.html)
[Glue tool](https://guitarvydas.github.io/2021/04/11/Glue-Tool.html)

# See Also

[Blog](https://guitarvydas.github.io)
[Videos](https://www.youtube.com/channel/UC2bdO9l84VWGlRdeNy5)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
