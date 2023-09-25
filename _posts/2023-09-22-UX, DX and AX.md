
UX means User eXperience.

DX means Developer eXperience.

AX means Academic eXplanation.

The goal is to understand programming principles in a rigorous manner.  Then, to sugar-coat these principles in a way that is palatable to programmers who "just want to solve a problem and get the solution to work" without having to learn the academic details and nuances.  Then, to sugar-coat the solutions in ways that allow end-users to "just use the app to get their work done" (where the work usually does not involve thinking about programming, nor the nuances of academic analysis of programming).

## Example - Loops
It is now clear that the most rigorous way to write iterative code is to use recursion.

But, programming practitioners like to think in terms of less-rigorous constructs, such as *loops*.

Currently, we force programming practitioners to bend their thinking habits away from *loops* and towards the more rigorous concepts of *recursion*.

Programming practitioners are forced to spend years in school to learn how to use *recursion* instead of *loops*, and, instead of learning more about how to ply their trade of composing real, workable solutions, to real-life problems.

### Suggestion
A suggestion arising from this observation is that maybe we need to create a syntax for *loops* that maps easily to *recursion* and can be tightly checked.

For example, maybe:

```
f :: procedure (items : ListOf[integer]) {
  loop over items -> item {
      termination: empty;
      iteration: 
        do-something1-with (item); 
        do-something2-with (item);
    }
}
```
Where the `iteration` case is automagically expanded to recur with the rest of the list.

Where the `iteration` case is automagically optimized for lists represented as arrays (CDR-less lists) and generalized to handle general lists (with CDRs).

The above piece of code might be transpiled to Common Lisp as:

```
(defun f (items)
  (mapc #'(lambda (item) 
            (progn 
              (do-something1-with item) 
              (do-something2-with item)))
        items))
```

and maybe to something similar in JavaScript, like:

```
function f (items) {
  items.forEach (item =>  {
      do_something1_with(item));
      do_something2_with(item));
    });
}
```

## See Also
### Blogs
https://publish.obsidian.md/programmingsimplicity (see blogs that begin with a date 202x-xx-xx-)

https://guitarvydas.github.io/
### Videos
https://www.youtube.com/@programmingsimplicity2980
### Books
leanpub'ed (disclaimer: leanpub encourages publishing books before they are finalized)
https://leanpub.com/u/paul-tarvydas
### Discord
https://discord.gg/Jjx62ypR  ("programming simplicity") all welcome, I invite more discussion of these topics
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
