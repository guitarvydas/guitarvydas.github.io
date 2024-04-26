# Embedding Code Snippets in New Syntaxes

In general, I write *t2t* - text-to-text converters - that address a specific issue instead of writing a whole new language from scratch. I generate code for some host language, then let the host language compiler do the heavy lifting.

For example, I might create a syntax for control flow, like Statecharts, that uses embedded Javascript to handle most of the bits of programming that don't need to be redefined.

A particular example of this is the `.rwr` syntax for my RWR ("ReWRiter") DSL for helping me write DSLs.

In RWR, a rewrite string is a string of characters and string interpolations surrounded by Unicode quotes `‛...’`. Using separate characters for "open" and "close" just makes parsing this easier with OhmJS and PEG. Unicode has so many characters that we can afford the luxury of cherry-picking characters that we want to use and to hard-code their meaning forever. ASCII is limited to 96 characters (printables other than whitespace and control characters), so you are - subtly - reluctant to waste ASCII characters in this way, and, instead, you do hard-to-parse things like re-using `"` to mean string-begin AND string-end. This, also, blocks recursive pattern matching like that in PEG.

In an RWR rewrite string, any ASCII character is valid and is simply copied to the output.

The special Unicode brackets `«...»` signify a string interpolation. The `...` can be any valid Javascript expression. Usually, you say `«x»` to mean "insert the value of the Javascript variable `x` at this point", but, sometimes you say `«fn(y)»` to mean "call the function `f` with parameter `y` and insert the returned string here."


# Example 1

The following rewrite string:

```
`function «name» () { «code» }’
```

Might be rewritten as:

```
function rewrite (name, code) {
    return `function ${name} { ${code} }`;
}
```

The above is legal JS, where the string returned by the function is a Javascript *template* string. In a template string, anything surrounded by `${...}` is evaluated and results in a character string.

A working version of the code (run `make` in [embeddingsnippets](https://github.com/guitarvydas/embeddingsnippets/tree/main))...

```
function rewrite (name, code) {
    return `function ${name} (x, y) { ${code} }`;
}

console.log (rewrite ("f", "return x + y;"));
```

output is:
```
function f (x, y) { return x + y; }
```
# Example 2

```
let counter = 42;
function gensym (basename) {
    let n = counter;
    counter += 1;
    return `${basename}_${n}`;
}

function rewrite (name, code) {
    return `function ${gensym (name)} (x, y) { ${code} }`;
}

console.log (rewrite ("f", "return x + y;"));


```

output is:
```
function f_42 (x, y) { return x + y; }
```

# More

Of course, you can go nuts and start using the comma operator to string multiple expressions together, using the value of only the last one.

```
let counter = 42;

function gensym (basename) {
    let n = counter;
    counter += 1;
    return `${basename}_${n}`;
}

function rewrite (name, code) {
    return `function ${counter = 100 , gensym (name)} (x, y) { ${code} }`;
}

console.log (rewrite ("f", "return x + y;"));

```

output is:
```
function f_100 (x, y) { return x + y; }
```

# Ohm
A grammar for the above can be defined as:
```
simple_rwr {
  rewriteString = "‛" c* "’"
  c =
    | "«" inner_c+ "»" -- interpolation
    | inner_c          -- raw
  inner_c = ~"‛" ~"’" ~"«" ~"»" any
}
```
![embeddingohm.png](/assets/embeddingohm.png)
# RWR
And the RWR for the above grammar is
```
simple_rwr {
  rewriteString [lq c* rq] = ‛«lq»«c»«rq»’
  c_interpolation [lb c+ rb] = ‛«lb»«c»«rb»’
  c_raw [c] = ‛«c»’
}
```
[TBD - I haven't implemented this bit yet and got it to run. I will be developing this using the existing drawware tools and the existing 'transpile' component. Keep in touch. Collaborators welcome.]
# Appendix - See Also

### References

[https://guitarvydas.github.io/2004/01/06/References.html](https://guitarvydas.github.io/2024/01/06/References.html)

### Blog
[blog](https://guitarvydas.github.io/)

### Blog
[obsidian blogs](https://publish.obsidian.md/programmingsimplicity) (see blogs that begin with a date 202x-xx-xx-)
### Videos
[videos - programming simplicity playlist](https://www.youtube.com/@programmingsimplicity2980)
### Pamphlets
[DSL for Writing DSLs](https://tarvydas.gumroad.com/l/hiypq?_gl=1*1bdn1r0*_ga*NTI5MDkzNTI0LjE3MTAzNTQzNjU.*_ga_6LJN6D94N6*MTcxMTQ4ODE0Mi43LjAuMTcxMTQ4ODE0Mi4wLjAuMA..)

[Is Concurrency Difficult?](https://tarvydas.gumroad.com/l/dvtej?_gl=1*o7hy6z*_ga*MjA0NzUyMDY1Mi4xNzA3NDc3MDIx*_ga_6LJN6D94N6*MTcwNzQ3NzAyMC4xLjEuMTcwNzQ3NzI5Ni4wLjAuMA..)
### Discord
[Programming Simplicity](https://discord.gg/Jjx62ypR) all welcome, I invite more discussion of these topics, esp. regarding Drawware and 0D
### Twitter
@paul_tarvydas
### Books (WIP)
[leanpub](https://leanpub.com/u/paul-tarvydas)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
