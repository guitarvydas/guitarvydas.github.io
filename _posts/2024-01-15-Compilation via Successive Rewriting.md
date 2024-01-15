These are rough notes regarding the technique of Syntax-Directed Transpilation.  In other places, I have called this *nano-parsers* and *divide-and-conquer*, etc. I try to present ideas by writing out snippets of code and intermediate code, but, none of the code has actually been tested. The technique is more important than the code itself...

- textual rewrites, *only* 
- only the first grammar needs to be human readable, the intermediate grammars need only be parsable by a machine and we don't care if humans like them or not

See the final section "Suggested Approach" for suggestions on how to proceed to explore this technique.
# Legend

`⎡ s1 ⎤` 
   - begin scope "s1"

`⎣ s1 ⎦` 
   - end scope "s1"

`⟪+ name="ch",kind=channel,scope=global,value=5⟫` 
   - data descriptor (def datum)
   
`⟪name="ch",kind=channel,scope=global,indirection=1,value=5⟫` 
   - data descriptor usage (datum usage)

`š`
- marker for subroutine operation

I use Unicode symbols in the intermediate code to avoid characters that might be used in the current crop of 3GL programming languages (JS, Python, Rust, WASM, assembler, etc.).  Note that my tool of choice - OhmJS - can accept Unicode symbols.  PEG parsing, which OhmJS is based on, can parse bracketed pairs, so I tend to use various kinds of Unicode brackets.

goals:
- first few passes gather up semantic info
- somewhere along the way, a pass replaces ALL variables with data descriptors
- another pass checks that the data is being used legally
- last pass transpiles (the now, known to be OK) code to *language of your choice*

# pass 0

Human readable source code is input into the compiler pipeline ...

```
package main
import "fmt"
def ch 5
func main() {
    defint i 42
    fmt.Printf("Hello World channel=%d i=%d\n", ch, i)
}
```

# pass 1 - semantic gathering of scope info
```
⎡ s0 ⎤
  package main
  import "fmt"
  def ch 5
  func main()
    ⎡ s1 ⎤
      defint i 42
       fmt.Printf("Hello World channel=%d i=%d\n", ch, i)
    ⎣ s1 ⎦
⎣ s0 ⎦
```

N.B. - braces are now syntactic noise and have been removed

# pass 2 - semantic gathering of package info
```
⎡ s0 ⎤
⟪+ name="main",kind=package,scope=package,value=?⟫
import "fmt"
def ch
func main()
  ⎡ s1 ⎤
    defint i 42
     fmt.Printf("Hello World channel=%d i=%d\n", ch, i)
  ⎣ s1 ⎦
⎣ s0 ⎦
```

# pass 3 - semantic gathering of function info
```
⎡ s0 ⎤
⟪+ name="main",kind=package,scope=package,value=?⟫
import "fmt"
def ch
⟪+ name="main",kind=function,scope=subroutine,value=??,number-of-formals=0,formals=❲❳⟫
  ⎡ s1 ⎤
    defint i 42
     fmt.Printf("Hello World channel=%d i=%d\n", ch, i)
  ⎣ s1 ⎦
⎣ s0 ⎦
```

N.B. If the function had more than 0 formal parameters, I guess each one would eventually be replace by a data descriptor (like, below in "semantic gathering of variables info")
# pass 4 - semantic gathering of variables info
```
⎡ s0 ⎤
⟪+ name="main",kind=package,scope=package,value=?⟫
import "fmt"
⟪+ name="ch",kind=channel,scope=global,value=5⟫,
⟪+ name="main",kind=function,scope=subroutine,value=??,number-of-formals=0,formals=❲❳⟫
  ⎡ s1 ⎤
     ⟪+ name="i",kind=int,scope=s1,value=42⟫)
     fmt.Printf("Hello World channel=%d i=%d\n", ch, i)
  ⎣ s1 ⎦
⎣ s0 ⎦
```

Comment: I don't know what to do with the import information, I haven't thought about this nor tested it. Actually building and using this stuff will probably require changes. Maybe *imports* cause another file to be pasted in?
# pass 5 - semantic replacement of variables
```
⟪+ name="main",kind=package,scope=package,value=?⟫
import "fmt"
⟪+ name="main",kind=function,scope=subroutine,value=??,number-of-formals=0,formals=❲❳⟫
     fmt.Printf(
       ⟪name="",kind=string,scope=s1,value="Hello World channel=%d i=%d\n",indirection=0⟫,
       ⟪name="ch",kind=channel,scope=global,value=5,indirection=1⟫,
       ⟪name="i",kind=int,scope=s1,value=42,indirection=1⟫
    )
```

N.B. variable refs now contain *indirection* level, kinda like `*` in C, where 1 means "normal", 0 means *constant*, 2 means indirect once (`*var`), 3 means indirect twice (`**var`) and so on. Normal indirection is 1 - i.e. suck value out of memory location.

N.B. The scoping brackets have been deleted - the required info has been embedded in the data descriptors

N.B. variable datadesc defs have been deleted - no longer needed. The other defs (package, function, etc.) should probably disappear, but I haven't figured out the details.

# pass NN - replacement of operations
```
⟪+ name="main",kind=package,scope=package,value=?⟫
import "fmt"
⟪+ name="main",kind=function,scope=subroutine,value=??,number-of-formals=0,formals=❲❳⟫
     š "fmt.Printf" number-of-args=3
	     (
	       ⟪name="",kind=string,scope=s1,value="Hello World channel=%d i=%d\n",indirection=0⟫,
	       ⟪name="ch",kind=channel,scope=global,value=5,indirection=1⟫,
	       ⟪name="i",kind=int,scope=s1,value=42,indirection=1⟫
	    )
```

# pass MM - transpile to code
[tbd]
- can you transpile pass NN using OhmJS/ChatGPT/etc?
- can you write out code that some other compiler (e.g. Go, JS, Python, Odin, Rust, WASM, etc.) can compile and execute?

# Suggested Approach
Write an OhmJS grammar that parses the intermediate code labelled "Pass NN" above.  Use the grammar to emit code in *your favourite language* (e.g. JS, Python, Go, Odin, Rust, WASM, etc., etc.).  My target language of choice is something based on Lisp (Common Lisp, Scheme, Racket, etc.), because it has almost no syntax to get in the way. Lisp's recursive syntax often requires one to write parsing rules that are recursive (this is a good habit, anyway).

When this part is working, back up one pass and try to get it working.  And, so on until you reach Pass 0.

# Appendix - See Also

### References

[https://guitarvydas.github.io/2004/01/06/References.html](https://guitarvydas.github.io/2024/01/06/References.html)

### Blogs
[blog](https://guitarvydas.github.io/)

[obsidian blogs](https://publish.obsidian.md/programmingsimplicity) (see blogs that begin with a date 202x-xx-xx-)
### Videos
[videos - programming simplicity playlist](https://www.youtube.com/@programmingsimplicity2980)
### Books
leanpub'ed (disclaimer: leanpub encourages publishing books before they are finalized - these books are WIPs)
[Programming Simplicity Takeaways, and, Programming Simplicity Broad Brush](https://leanpub.com/u/paul-tarvydas)
### Discord
[Programming Simplicity](https://discord.gg/Jjx62ypR) all welcome, I invite more discussion of these topics, esp. regarding Drawware and 0D
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
