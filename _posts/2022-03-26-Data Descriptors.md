---
layout: post
title:  "Data Descriptors"
---
# Data Descriptors - Normalization
One aspect of normalization is the normalization of data locations[^controlflow].

[^controlflow]: As opposed to control flow.  Dataflow and Control flow are orthogonal.

Holt created the concept of *data descriptors* and Cordy used data descriptors in his OCG (Orthogonal Code Generation) work.

The point of creating data descriptors is to describe every data location in the *same* way - i.e. normalization.

Normalized form - for anything - makes it easier to manipulate the form.  The manipulation can be done by a machine (a compiler).

There is nothing particularly magical about normalization or manipulation.  To create a normalized form you just need to survey the problem space and choose an umbrella form that can be used to describe any item in that space.

## Components of Data Descriptors

Data descriptors, as originally described, are 5-tuples:
- k - a level of indirection (k <= 2 in the original form)
- b - an abstract base, a code that represents a register or a region of memory (like .bss or a lexical level)
- d - a displacement from the base
- x - an index
- s - a scale factor

Data descriptors can be written as:
@^kb.d[x.s]

### Example 1
If we want to describe a 1-byte item pointed-to by register R0, we might write

@^1R0.0[0.1]

[C doesn't let us specify registers directly, so we can't write this in high-level C].

### Example 2
If we want to describe a 1-byte item pointed-to by the Stack Pointer, we might write:

@^1SP.0[0.1]

In C, we might write

```
{ 
  unsigned char name;
  name;
}
```


### Example 3
To write a DD referring to a byte pointed-to by a C pointer in a variable on the stack, we might write

@^2SP.0[0.1]

or, in C

```
{
  unsigned char *p;
  *p;
}
```

[So, how does the compiler know the size of addresses?  It doesn't know this, nor does it need to care.  This is all worked out by the Allocator.  See below.  That's the beauty of normalization - divide and conquer.]

### Example 4

To refer to a byte passed as a parameter, we might write

@^1AP.0[0.1]

where `AP` is some register used for pointing at parameters (probably on the stack).

or in C:
```
void f (char *p) {
*p;
}
```

### Example 5

In C, we might write
```
void f (int x) {
  long y;
  y = x;
}
```

and might re-write this in DD form as:

@^1LP.0[0.4] = @^1.AP.0[0.2]

where ints are 2 bytes and longs are 4 bytes, and,

LP is a register that points to parameter variables (probably on the stack) and AP is a register that points to the parameters (probably also on the stack).

[Aside: note that most of the syntactic "noise" has been removed.  This code looks ike data descriptors instead of C code..  Each pass helps the next pass out by stripping noise and details out of the program.]

### Example 6

In C, we write
```
int main (int argc, char **argv) { 
... 
}
```
The parameters to main are
1. argc (an int)
2. argv (a pointer to a pointer of chars)

And, the return value of `main` is an `int`.  Let's say that `int`s are 2 bytes long.

The return value of `main` is representd by
@^1SP.0[0.2]

and the parameters are

argc : @^1AP.0[0.2]

argv : @^1AP.1[0.4]

where addresses are 4 bytes long and ints are 2 bytes long.

The character at `\*\*argv` is

@^2AP.1[0.1]

### Example  - Constant
```
{ 
int y;
y = 8;
}
```

Might be written as

@^1LP.0[0.2] = @^0-.8[0.-]

or

{1,"LP",0,0,2} = {0,"-",8,0,"-"}

## Allocator

The compiler does not care *where* data ends up.

The *allocator* makes the decision.

The compiler only states that a variable is relative to some Lexical Base.

The Allocator fixes that up.

The *allocator* is like a mid-level loader.

IMO, compilation is not a binary process, but a pipeline of successive refinements.  The compiler feeds the allocator.   The allocator feeds the loader.  And so on.  

IMO, the whole process is a continuum.  IMO it is meaningless to talk about a *compiler* and a *linker*.  Each stage in the pipeline compiles a bit, then passes the result off to the next stage, which compiles a bit more, and so on.

Compilation, is itself, just a parial optimization.  A compiler checks and strips some information from the program, then passes the stripped program on to the next phase in the pipeline.

The goal of compilation is to strip out as much information as possible, to allow the compiled program to run as fast (or as small) as possible on the target machine.

## Original Paper
[Data Descriptors - a compile-time model of data and addressing](https://dl.acm.org/doi/10.1145/24039.24051)
## See Also
[Names and Data Descriptors](https://guitarvydas.github.io/2022/03/24/Names-and-Data-Descriptors.html)

[Data Descriptors - a compile-time model of data and addressing](https://dl.acm.org/doi/10.1145/24039.24051)
[OCG](https://books.google.ca/books/about/An_Orthogonal_Model_for_Code_Generation.html?id=X0OaMQEACAAJ&redir_esc=y)

[Table of Contents](https://guitarvydas.github.io/2021/12/10/Table-of-Contents-Dec-01-2021.html)
[Blog](https://guitarvydas.github.io)
[Videos](https://www.youtube.com/channel/UC9EJr0nKHwadbHUtc5zHdmQ/videos)
[References](https://guitarvydas.github.io/2021/01/14/References.html)
[Books](https://leanpub.com/u/paul-tarvydas.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" > 
</script> 