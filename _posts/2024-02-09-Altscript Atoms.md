| altscript | Lisp (Scheme, Racket, Common Lisp) |
|-----------|--------------------------------------------------------------|
| `123`      | (integer 123)
| `1.23`     | (decimal-floating-point 1 23)
| `1,23`     | (decimal-floating-point-european 1 23)
| `$1.23`    | (currency 1 23)
| `1.2.3`    | (tuple 1 2 3)
| `1..20`    | (range 1 20)
| `12x340`   | (pair 12 340)
| `#1A2B`    | (hex "1A2B")
| | |
| `2021-4-5`  | (date 2021 4 5)
| `10:23:45`  | (time 10 23 45)
| `2021-4-5-10:23:45` | (date-and-time 2021 4 5 10 23 45)
| `2021-4-5-10:23:45-8:00` | (date-and-time-and-timezone 2021 4 5 10 23 45 8)
| | |
| `"abc"`    | (string "abc")
| `''abc''`  | (long-string "abc")
| `<abc>`    | (html-tag "abc")
| `%abc`     | (path "abc")
| `abc://`   | (url "abc://")
| `ab@cde`   | (email "ab@cde")
| `#"a1b2c"` | (binary-hex "a1b2c")
| `##"atbfc"` | (binary-b64 "atbfc")
| | |
| `abc`  | (word "abc")
| `abc:` | (def-word "abc")
| | |
| `:abc` | (get-word "abc")
| `'abc` | (symbol "abc")
| `.abc` | (selector "abc")
| `/abc` | (refinement "abc")
| `@true` | (true)
| `@false` | (false)
| `@none` | (none)
| `@litstring` | (litstring)
| `@nan` | (nan)
| | |
| `abc.def`  | (field "abc" "def")
| `abc.def:` | (set-field "abc" "def")
| `:abc.def` | (get-field "abc" "def")
| `abc/def`  | (frefinement "abc" "def")


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
