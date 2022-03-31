---
layout: post
title:  "Modeling vs. Compilation"
---

## Various Paradigms for Various Folks

### Spreadsheets

If someone wants to think about bookkeeping and balance sheets and income statements, they use a spreadsheet.

### JavaScript

If someone wants to think about creating websites for commerce, they use JavaScript[^js].

[^js]: You would think that there must be something better than JS, but strongly-typed languages ain't it.  The website problem involves distributed programming, and we don't (yet) have suitable languages to express that kind of problem easily.  We need to get rid of synchrony, first.

### Lambda Calculus

If someone wants to think about the nuts-and-bolts of programming languages, one uses Lambda Calculus.

### Lambda Calculus vs. JavaScript vs. Spreadsheets

Spreadsheet thinkers don't want to express the detail required to write JavaScript programs.

JavaScript programmers don't want to express the detail required to write Lambda Calculus.

Lambda Calculus thinkers don't want to use Excel® (a spreadsheet language) to think about the kinds of things they think are important.

What is important to Lambda Calculus thinkers isn't important (too detailed at a micro-managed level) for CFOs.

### Conclusion - There Can't Be One Paradigm To Rule Them All

If you think that *your* paradigm is the *final answer* to the programing problem, then you are mistaken.

It's "turtles all the way down".  

Once you've found a suitable simplification, you can re-simplify it to express new problem domains.

#### Fads

Another way of saying that *your paradigm is the best one* is to use the word *fad* to describe your paradigm.

## Models vs. Compilers

Computers allow us to automate transpilation.

Models can be converted (compiled, transpiled) to executable code.

Think compilation, not model.

Thinking about models is too "airy fairy" for for machine-generation.

If you have a model, try to tell a machine how to convert that model into executable code.

High Level Languages are models of computation.  Compilers tell the machine how to convert such models to executable code.

Assemblers are models of micro-coded CPU architectures.

Micro-coded CPU architectures are models of transistor systems.

Transistor systems are models of semi-conductors.

Semi-conductors are models of chemical oxides.

Molecules are models of atomic structures.

Atoms are models of sub-atomic structures.

It's turtles all the way down.

If you want a machine to convert a model automatically, you have to tell the machine how to do this.

We used to be restricted to writing our models down on pieces of paper.

Now, we can create models that have more possible dimensions.

Now, we can tell machines how to transpile the models into lower-level models.

Thinking *only* *about *models* is the lazy way out.  It's only half the job.  You need to explain to a machine how to convert the model into a lower-level form.

I use the word "notatation" to mean "models that can be compiled into lower-level form". 

We - the royal we - started to think about how to get machines to convert our notations.  Then, "we" invented compilers and essentially stopped thinking about the conversion process, in lieue of improving our models (which is only half the job).

There *have been* some advances on the machine-conversion front, e.g. PEG, bits of lambda calculus, etc.

A lot more effort has been placed on the optimization front, instead of the "what else can we say?" front.

## See Also

[Table of Contents](https://guitarvydas.github.io/2021/12/10/Table-of-Contents-Dec-01-2021.html)
[Blog](https://guitarvydas.github.io)
[Videos](https://www.youtube.com/channel/UC9EJr0nKHwadbHUtc5zHdmQ/videos)
[References](https://guitarvydas.github.io/2021/01/14/References.html)
[Books](https://leanpub.com/u/paul-tarvydas.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" > 
</script> 