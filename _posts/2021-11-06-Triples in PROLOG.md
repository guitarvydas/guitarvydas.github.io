---
layout: post
title:  "Triples in PROLOG"
---

# Minor Revelation
I used to think of triples in PROLOG (Datalog, etc.) to be something like
```
relation(subject,object).
```
but, PROLOG makes it hard to pattern-match on `relation`.

For example, if I want to `find all relations that include a specific subject`, then, the above format makes it difficult to express the query.

Instead, maybe a triple should be represented as
```
triple(relation,subject,object).
```
?

# WIP

I am going to try this new format for a while...

I'm going to use the keyword `fact` to denote a triple.

```
fact(relation,subject,object).
```

# SWIPL Dicts

SWIPL includes an extension to classical PROLOG, in the form of [dict objects](https://www.swi-prolog.org/pldoc/man?section=bidicts).

This might be something else to investigate.

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
