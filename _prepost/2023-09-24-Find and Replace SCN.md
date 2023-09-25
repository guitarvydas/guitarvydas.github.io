![[/screenshots/Find and Replace.png]]
WIP: playing with Ohm-JS / PEG operations ; using Obsidian markdown editor + a bit of HTML...

- Loop is a main rule - included in macro processor
- bulleted rules are helper rule for the main rule
- ASCII words are become Ohm-JS quoted strings "..."
- subscripted, italicized names are rule-calls
- ↺ represents recursion operator, i.e. Clause #nested parses `{` , calls rule `Statement`, `}`, then calls itself optionally (`?`)
- underlined patterns represent bracketed matches, subscripted by `1...` or `0...` or `?` translating to `+`, `*`, and `?` Ohm-JS iteration operations
- `≠`translates to `~` in Ohm-JS, i.e. negative match of next item
	- e.g. `≠;` means `not semicolon` (~";")
- `✓` translates to `any`
- `=` means `same as`, translates to a single rule call
	- e.g. "<mark>SymbolListName</mark>       `=` <sub><i>word</i></sub> " translates to "SymbolListName = word" 
- tags translate to `-- tag` in Ohm-JS
	- e.g.  "- <mark>Clause</mark> #nested ...""  translates to "Clause = | ... -- nested"


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

