---
layout: post
title:  "FDD In Action"
---

"FDD" means "Failure Driven Design".

FDD can prevent future bugs.

FDD is like “design rule” checking built into the dev app.

I spent hours tracking down a hoary bug in my logic.

I wrote:
```
… (Kind, Edge, edge)
… sourceof(Edge, Sender)
… targetof(Edge, Receiver)
… (direct_contains, Parent, Edge)
```  
Which failed silently using PROLOG rules.

The final clause “… (direct_contains, Parent, Edge)” was not fulfufilled due to a bug in my logic - the outer-most container did not have a Parent.

Nothing could prevent me from making this mistake, but, it is possible to prevent _other_ errors of this kind.

# What I Wanted to Say
I wanted to say:

```
Forall “… (kind, Edge, edge)”, and, 
 There must be a fact “… sourceof(Edge, Sender)”, and,
 There must be a fact “… targetof(Edge, Receiver)”, and,
 There must be a fact “… (direct_contains, Parent, Edge)”
else
 fail loudly
 ``````
 
# What I Really Said

But, I wrote:
```
Forall “… (Kind, Edge, edge)”
 And, if there is a fact “… sourceof(Edge, Sender)”,
 And, if there is a fact “… targetof(Edge, Receiver)”,
 And, ifthere is a fact “… (direct_contains, Parent, Edge)”
 succeed
```
# What's the Difference?
A subtle difference.  

The And version silently fails if ANY of the 4 clauses is false.

Subtle bugs are the hardest to find. 

# Preventing Errors Using FDD

Using FDD mentality, I can change the meaning of:
```
… (kind, Edge, edge)
… sourceof(Edge, Sender)
… targetof(Edge, Receiver)
… (direct_contains, Parent, Edge)
```
  
To mean what I wanted and simply push a button to regenerate the whole shebang, and, raise errors for any other latent bugs of this nature.

## Example Design Rule Check

I can choose syntax to map to meaning - I might change the generated code to match what I wanted to say.

For example, I might generate code that matched the first clause, then asserted the rest of the clauses (with appropriate error messages), e.g.

```
… (kind, Edge, edge)
(… sourceof(Edge, Sender)” -> true ; format(user_error, “FAILURE sourceof(Edge,Sender) failed on ~w~n)”, [Edge])
(… (targetof(Edge, Receiver) -> true ; format(user_error, "FAILURE:targetof(Edge, Receiver) ~w~n)", [Edge])
(… (direct_contains, Parent, Edge)” -> true ; format(user_error, "FAILURE: direct_contains, Parent, Edge) ~w~n)", [Edge])
```
The above code looks horrible and hides the true essence of what I want to say, but, the machine doesn't care and will check my other code for errors.

I'm using PROLOG (swipl) as *assembler* and I'm emitting assembler code (PROLOG) to do what I want.

I can modify the DSL syntax, push a button, and have ALL of my code checked.  

I don't need to look at the generated assembler code (PROLOG)[^30].

[^30]: The only reason to look at the generated assembler is to debug the transpiler.  Once debugged, no one needs to look at the assembler.

Yes, there might be cases where I want to say AND instead of "there must be a fact".  I will modify (invent) the syntax to handle such cases.  I expect that most of my code is based on "there must be a fact" rules, with AND rules being the exception.  I intend to invent a syntax to express AND rules, and, I will use the FDD transpiler to find those cases for me (in the current code base).

FDD lets me make sweeping changes such as this.   

I need to modify the transpiler, then I need to push a button (or invoke `./run.bash`).

Not a lot of work, but it captures one of my pervasive errors in logic...

Yes, I *could* have written the code correctly in the first place, but that would require a lot more thinking on my part (and, probably, a PhD degree).

I said what I wanted to say.  Now, using FDD, my only task is to make the computer (transpiler) *do* what I wanted...
# See Also

[FDD - Failure Driven Design](https://guitarvydas.github.io/2021/04/23/Failure-Driven-Design.html)

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
