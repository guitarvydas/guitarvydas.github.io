---
layout: post
title:  "Software Components 101 - Part 11 Starting Over"
---

# Do What I Say

In trying to solve the problem in chapter 10, I realized that I'm not following my own advice.  

I'm not simplifying enough.

At this point, we will throw everything away and start again.

We can do this because we haven't written much code.

We aren't throwing away the _thinking_, just the code.

We have learned more about the problem that we didn't know at first.

# FDD
This is FDD - Failure Driven Design.

We can change our minds about the Architecture at the drop of a hat.

# Diagrams Should Be Simple
Our diagrams contain
1. rectangles
2. ellipses
3. arrows (lines)
4. text.

We will write simple grammars that convert such simple diagrams into factbases.

From there, we will use inferencing to derive all other interesting information.

See, also, the essay "Diagram Conventions"
# Un-Nest Diagrams
One of the existing complications is that we chose to allow nested diagrams.

Let's stop doing this.  

Diagram "v" should consist of 4 diagrams
1. v
2. v-x
3. v-x-y
4. v-x-y-z

# Rewrite Diagrams in Markdown
We rewrite the diagrams in markdown.  

For example, diagram v is written in markdown as:
```
# rect v
## shape rounded
## color F5F5F5FF
## circle v/a
## circle v/d
## rect v/b
### shape rounded
### rect v/b/a
#### color green
### rect v/b/b
#### color green
### ellipse v/c
### rect v/x
#### color E3E3E3FF
#### shape rounded
#### rect v/x/a
##### color green
#### rect v/x/b
##### color green
#### rect v/x/c
##### color yellow
## arrow v/a v/x/a
## arrow v/a v/b/a
## arrow v/b/b v/c
## arrow v/c v/x/b
## arrow v/x/c v/d
```

See the final versions of the diagrams in `v.md`, `v-x.md`, `v-x-y.md`, and, `v-x-y-z-.md`.

## Emacs Elides Markdown
Emacs elides markdown in Org-mode manner.

This makes it easier to eye-ball the the .md files.

# De-Indenting Markdown, De-Indenting Python, De-Indenting ORG Mode

The next step is to convert indentation-based syntax into nested syntax.

This conversion should be easy to apply to Python code and to org-mode documents.

See Part 12.

## Python
Exercise: Write a program that converts Python code to nested code using REGEX in any programming language. 

Exercise: Write a program that converts Python code to nested code using `grasem` (hint: look ahead to part 12).

### Example 
(Python code lifted from https://www.w3schools.com/python/python_functions.asp))
```
def my_function():
  print("Hello from a function")
```
should be rewritten as
```
def my_function() {
  print("Hello from a function")
}
```
## Org Mode
Exercise: Write a program that converts an org-mode document to a nested document using REGEX in any programming language.  Skip this exercise if you used REGEX to convert Python code, in the above exercise. 

Exercise: Write a program that converts an org-mode document to a nested document using `grasem`.

### Example
```
* def my_function():
** print("Hello from a function")
```
should be rewritten as
```
def my_function() {
  print("Hello from a function")
}
```


<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
