
I've been hoping to try (or get someone else to try :-) using Excalidraw as a front end. 

Aside: in my earlier experiments, I used CL to parse the XML and then punted to Prolog to infer missing information. Prolog rules could recognize "intersection" and "bigger"/"smaller" rectangles which then produced containment relationships. Something like "this rectangle is smaller than that rectangle, so this rectangle must be a port, and, this rectangle intersects an edge of the bigger rectangle, so it must be a port that belongs to the bigger rectangle". And "what is the prototype name of the bigger rectangle? Answer: this text box is completely within the bigger rectangle, but outside of all other rectangles, so this text box must contain the prototype name of the bigger rectangle". And, likewise, with arrows - "this arrowhead nearly touches that box, which has already been determined to be a port, hence, this arrow must feed into the port". Etc., etc. Draw.io's file format supplies you with that information, so Prolog isn't needed there, but, other drawing tools don't supply you with that info, so you have to infer it from various - simple - relationships (intersects, contained, above, below, to left of, to right of, etc.).  

Using only such simple relationships - that any high-schooler has the math chops to calculate - one might devise other interesting syntaxes. The conversion from draw.io to JSON is boooring and repetitive and niggly to code up. Maybe so boring that it might be punted to an LLM, instead of wasting human time? 

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
