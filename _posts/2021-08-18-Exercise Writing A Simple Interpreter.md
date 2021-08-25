---
layout: post
title:  "Exercise Writing A Simple Interpreter"
---

# Exercise
Write a simple interpreter that parses a simple language and calls functions to do the actual work.

## Syntax
```
fork
krof
dup N
push N
exec1st args
exec args
redir N
pipes N
```
N is a small integer.

Args is a string of characters, possibly including spaces, until end-of-line ('\n').
## Functions
```
void push (string)
int pop ()
void gdup (string)
void redirect (string)
doFork (...)
doExec (...)
```
# Appendix Answer: A Simple Interpreter In C
This interpreter is also implemented in [grash](https://github.com/guitarvydas/vsh/tree/master/grash) with some embelishments.
```
...
char *parse (char *cmd, char *line) {
  /* if command matches, return pointer to first non-whitespace char of args */
  while (*cmd)
    if (*cmd++ != *line++)
      return NULL;
  while (*line == ' ') line++;
  return line;
}
...
int comment (char *line) {
  /* return 1 if line begins with # or is empty, otherwise 0 */
  return line[0] == '#' || line[0] == '\n' || line[0] == '\0';
}
...
void interpret (char *line, int argc, char **argv) {
  char *p;

  line = trim_white_space(line);

  if (comment (line))
    return;
...
    p = parse ("krof", line);
    if (p)
      exit(0);
    p = parse ("dup", line);
    if (p) {
      gdup (p);
      return;
    }
...
    p = parse ("push", line);
    if (p) {
      push (p);
      return;
    }
    p = parse ("exec1st", line);
    if (p) {
      doExec (p, argc, argv, 1);
      return;
    }
    p = parse ("exec", line);
    if (p) {
      doExec (p, argc, argv, 0);
      return;
    }
    p = parse ("redir", line);
    if (p) {
      redirect (p);
      return;
    }
    quit("can't happen");
    break;
...
    p = parse ("pipes", line);
    if (p) {
      mkPipes (p);
      return;
    }
    p = parse ("fork", line);
    if (p) {
      doFork ();
      return;
    }
    p = parse ("krof", line);
    if (p) {
	  ...
    }
...
}
```

# Appendix Simplicity (Discussion)

1. The syntax was chosen to be small and easy to implement.
2. Each command in the syntax takes exactly 0 parameters or 1 parameter.  (Where "args" is considered to be a single parameter.)
3. Simplicity is defined as "lack of nuance".  Every command takes a fixed number of arguments.  There are no commands that a variable number of arguments. There are no edge cases to consider.
4. The "args" parameter is not parsed and offers no resistance to the implementation of the interpreter.

# Appendix Optimization (Discussion)

The parser does brute-force matching of strings.

Brute-force matching of strings is "inefficient".

How "inefficient" can the parser be before optimization begins to matter?

The answer depends on 

1. how often the parser will run
2. the size of the inefficient code relative to the other code.

As it stands, the syntax is very small and the inefficiency of using brute-force string matching is small compared to the other work being performed.  

Specifically, in the case of *grash*, the main work consists of spawning operating system processes.   How much does it cost to spawn a process vs. how much does it cost to use brute-force string matching?

At present, it seems that spawning processes is much more costly than string-matching this syntax.  We could use a profiler to determine the exact ratio.

Optimizing this code should not stand in the way of just getting it to run correctly.

Later, when the code is put into production, Production Engineers can measure actual use-cases and determine whether optimization is necessary.

## Tokenizing Scanners

Most compiler-writers assume that their compilers will be used often and that the inefficiency of string-matching will be noticed by users of the compilers.

The first kind of optimization is to *tokenize* the incoming strings, using a hash table.  Tokenizing scans each incoming string once, and converts the string into a *token*.  *Tokens* are, basically, fixed-sized integers that are used as codes to represent the strings.  This allows later compiler passes to handle strings without performing more brute-force string matching - they simply perform brute-force code (integer) matching, which tends to be much more speedy than string-matching.

Strings appear only once in the compiler - in the hash table that maps tokens to strings.  This, also, constitutes a size saving (in general).

Note that Lisp does something similar when reading text.  Lisp reads input text using its *reader*.  In the process, Lisp tokenizes all incoming strings and calls these tokenize strings *symbols* instead of *tokens*.

Many interpreted languages do something similar.

Note that, when strings are tokenized, it doesn't matter how long (or short) a name is. It will be read only once and immediately converted into a *token*.  

All *tokens* are the same length.

## Appendix - Multiple Names For Items

It should be simple to add another level of indirection to *tokens*. Each *token* can represent a list of possible strings.  This arrangement would allow the IDE to show different names for any one named-item.  Experts might prefer to use single-character names in an algorithm, but novices (and anyone seeing the code for the first time, anyone trying to understand the algorithm) might see longer names at first.  The IDE might even allow users to "annotate" items with longer names (or complete phrases) as they go down the learning curve.

### Example

An example of this might be the equation for a line, which is commonly written in textbooks as:

```
y = mx + b
```

Experts might wish to view the equation using single-character names as:

```
y = m * x + b
```

whereas learners might wish to see embellishments, such as

```
y = slope * x + intercept
```



# Appendix Readability (Discussion)

Note that the syntax above is 

1. machine-readable
2. not very human-readable.

Many GPLs strive for human-readability.

Human-readability issues - like syntax, indentation, etc. - tend to cloud the ability to automatically manipulate programs.

To ease automatic manipulation of programs, it is less trouble to use machine-readable languages, like assembler, Lisp, etc.  

The concept of *macros* was invented using machine-readable languages.  

Human-readability tends to inhibit out-of-the-box thinking and the use of multiple paradigms in a single project.

# See Also

[Blog](https://guitarvydas.github.io)
[Videos](https://www.youtube.com/channel/UC2bdO9l84VWGlRdeNy5)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
