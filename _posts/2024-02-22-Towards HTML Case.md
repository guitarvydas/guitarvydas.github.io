Thinking... (WIP)...

I want to create IDs in programming languages that contain HTML formatting.  

For example, here is the formatted id "Collect".
```
<sub style="border-color: var(--border-color);">
  <font style="border-color: var(--border-color); font-size: 7px;">
    Collect
  </font>
</sub>
```

We learned to respect case in programming languages. Hence, we conclude that we should respect formatting in new programming languages.

In this case, the bare ID `Collect` should be considered to be different from the above ID.

The old ASCII rule - that an ID can contain no whitespace - doesn't apply to the above.

How do we parse such IDs? 

CFGs and REGEX can't do this job.

One possibility for parsing, is to use OhmJS/PEG to tokenize incoming text and to wrap some sort of marker brackets around each "token".

For example, we might tokenize the above as
```
❲
<sub style="border-color: var(--border-color);">
  <font style="border-color: var(--border-color); font-size: 7px;">
    Collect
  </font>
</sub>
❳
```

where the stuff between the Unicode brackets `❲...❳` is considered to be a whole ID token. Such IDs are the same only if they match character by character.  `❲Collect❳` is considered to be a different ID from the above formatted text.

Below is a specific example of what I'm working on at this moment:

```
ė
<sub style="border-color: var(--border-color);">
  <font style="border-color: var(--border-color); font-size: 7px;">
    Collect
  </font>
</sub>
<br style="border-color: var(--border-color);">
p.wallet += m.wallet
<br style="border-color: var(--border-color);">
m.wallet = 0
<br style="border-color: var(--border-color);">
⇒
```

I expect it to be tokenized as:

```
❲ė❳

❲<sub style="border-color: var(--border-color);">
  <font style="border-color: var(--border-color); font-size: 7px;">
    Collect
  </font>
</sub>❳

❲<br style="border-color: var(--border-color);">❳

❲p.wallet += m.wallet❳

❲<br style="border-color: var(--border-color);">❳

❲m.wallet = 0❳

❲<br style="border-color: var(--border-color);">❳

❲⇒❳
```

In this particular case, `❲ė❳` is a marker that is followed by an ID and then a bunch of formatted text. The ID is:

```
❲<sub style="border-color: var(--border-color);">
  <font style="border-color: var(--border-color); font-size: 7px;">
    Collect
  </font>
</sub>❳
```

and the rest of the text is
```
❲<br style="border-color: var(--border-color);">❳

❲p.wallet += m.wallet❳

❲<br style="border-color: var(--border-color);">❳

❲m.wallet = 0❳

❲<br style="border-color: var(--border-color);">❳

❲⇒❳
```

I can use OhmJS to tokenize in this manner. Are there any other existing tools that already do what I want? Can this suggested tokenizing format be altered to make parsing easier?

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
