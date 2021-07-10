---
layout: post
title:  "Indentation to Braces (Case Study)"
---

# Introduction
In this essay, I show how to build a little tranpsiler for debugging and code generation using a strategy I call the SCN Workbench[^scn].

This tool accepts 3 inputs:
1. Source code
2. Pattern matcher (aka grammar)
3. Output formatter (aka semantics).

The goal is to convert a notation to code, i.e. to build a transpiler.

The bare essence of the notation contains 2 lines, but blossoms into more than 100 lines when converted to code.

This is a case where the details overwhelm the basic simplicity of what is being done.

[^scn]: SCN means Solution Centric Notation.

# Disclaimer

I am currently debugging and re-writing the actual notation, but, the little helper transpiler works.

This note is about the little transpiler, not the final notation.

# Bare Essence

I want to build code to understand relative ids using UNIX-like "../" syntax.

The bare essence of what is needed is:
- set(rid val)
  c.ns[name] <= val
- get(rid).
  result <= c.ns[name]

(where `name` and `ns` are fields of the relative id).

Because I am debugging this concept, I'm lacing the code with error checks, checking for blunders and typos.

The error-check-laced pseudo-code is about 50 lines. The final code is about twice that.

# Layered Notation
The notation is intended to be layered.

For purposes of this essay, we can ignore the actual meaning of the notation and look only at the _shape_ of the notation.

At present the notation looks like:
```
getter (rid)
  result <= c.ns[name]
    where deconstruct rid => (_, ns, name)
    synonym c, component
    where component = @ea (rid)

setter (rid val)
  c.ns[name] <= val
    where deconstruct rid => (_, ns, name)
    synonym ns, namespace, "namespace within component"
    synonym c, component
    where component = @ea (rid)
    design rule "must not already have a value"

def (rid)
  @define all paths (rid)
  where
    define all paths (rid)
      ea (rid)

where
  ea (rid)
    ea-raw (rid) | design rule "must be a component" => result

  ea-raw (rid)
    typecase (rid.path)
    case string
      lookup (rid.path) => result
      design rule (result) "must not be empty"
    case _
      @getter (ref) => child
      child.static => result
	before 
	  where ref = rid.path
	  synonym ref, component-reference, "recursive reference to a component"
	  design rule (ref) "must contain a component namespace reference"



design rules

  rid must contain a component namespace reference (rid)
    "c" === rid.ns

  must be a component
    typeof (in) === "component"

  must not already have a value
    component.ns[name] === no-value
```

## Shape - First Impressions

The first things to notice about the notation is that
- it describes the problem in layers
- layers are written as indented code (Python-esque).

The first goal is to convert this notation into something more machine-readable.

For purposes of this essay, let's say that we want to convert the notation into:
```
getter (rid)
 {
 result <= c.ns[name]
  {
  where deconstruct rid => (_, ns, name)
  synonym c, component
  where component = @ea (rid)

 }
}
setter (rid val)
 {
 c.ns[name] <= val
  {
  where deconstruct rid => (_, ns, name)
  synonym ns, namespace, "namespace within component"
  synonym c, component
  where component = @ea (rid)
  design rule "must not already have a value"
 }
}
def (rid)
 {
 @define all paths (rid)
 where
  {
  define all paths (rid)
   {
   ea (rid)
   }
}
}
where
 {
 ea (rid)
  {
  ea-raw (rid) | design rule "must be a component" => result
  }
 ea-raw (rid)
  {
  typecase (rid.path)
  case string
   {
   lookup (rid.path) => result
   design rule (result) "must not be empty"
    }
  case _
   {
   @getter (ref) => child
   child.static => result
    }
}
 before 
  {
  where ref = rid.path
  synonym ref, component-reference, "recursive reference to a component"
  design rule (ref) "must contain a component namespace reference"
 }
}
design rules
 {
 rid must contain a component namespace reference (rid)
  {
  "c" === rid.ns
  }
 must be a component
  {
  typeof (in) === "component"
  }
 must not already have a value
  {
  component.ns[name] === no-value
 }
}
```
The above is less-readable from a human perspective, but more-readable from a machine-perspective.

In particular, the new version can be pattern-matched, using an automated pattern matcher like PEG.

# The Transpiler

The task of converting indented notation to braced-notation could be done in a number of ways, in fact a small Python program could do the job.

It is over-kill to use a parser for this task, but I will show how to do this nonetheless.

This example is small-enough to understand and will show the basics of using the SCN Workbench.

One of the aspects of FDD and notation-based thinking is to pick small, do-able tasks and to knock them off while reserving brain-power for the really big problem(s).

## The Pattern Matcher
The pattern match is written using a pattern-matching DSL[ohm].

The pattern matching DSL looks a lot like REGEXP, except that:
- it matches across lines
- the pattern match specification uses more than one line, whereas REGEXPs are usually a single line in length (or less).

I will present the pattern below, then discuss the details of the pattern.
```
ToBrace {

main = line+
line = indent? spc? toEOL* newline+
indent = (indentDoubleSpace | indentChar)+
indentChar = ("#" | "*" | "\t")
indentDoubleSpace = "  "
toEOL = ~newline any

newline = "\n"
spc = " "
}
```
Patterns consist of _rules_.  A _rule_ is usually about 1 line long.

_Rules_ in a pattern can refer to other _rules_.

The naming of the _rules_ is arbitrary, e.g. "main" is not special.

The first rule is taken to be the starting rule.

1. The rule _main_ matches one-or-more _lines_.
2. The rule _line_ matches an optional _indent_, followed by an optional _spc_ (my abbreviation for space), zero-or-more characters matched by the _toEOL_ rule and then one or more newlines
3. An _indent_ consists of an _indentDoubleSpace_ or an _indentChar_, one or more times `+`.
4. An _indentChar_ is either a "#" or a "*" or a tab ("\t").
5. An _indentDoubleChar_ is two spaces.
6. A _toEOL_ character is any character that is not a newline.
7. A _newline_ is "\n"
8. A _spc_ is " ".

It should be possible to write this rule as a REGEXP, or to write Python code to pattern-match lines.

Again, the point of this exercise is like a 'hello world' example: something painfully simple that shows the mechanics of the tool.

Parsing becomes more interesting when applied to larger examples, like a complete SCN.

Parsing matches structure, whereas REGEXP only matches lines.  This difference will become apparent later.

[^ohm] In this case, I use a DSL called Ohm-JS and build it into my SCN Workbench.

## The Outputter
The output spec consists of rules, also.

There must be exactly one output rule for each rule in the above pattern-match.

Each rule returns a string which is ultimately output by the workbench.

Each rule consists of 
- a name
- a set of parameters (enclosed in [])
- a "=" character
- an optional block of code (enclosed in double-braces `{{ ... }}`, which are similar to Liquid syntax[^braces])
- an output descriptor (`[[ ... ]]`)

The actual syntax and meaning of this format can be found in [the Glue tool](https://guitarvydas.github.io/2021/04/11/Glue-Tool.html)
```
main [@lines] = {{ resetBlock (); }} [[${lines}${emitclosebrace (0)}]]
line [@block @spc @chars @nl] = [[${emitopenbrace (block)}${emitclosebrace (block)}${spaces (block)}${chars}\n${shiftblock (block)}]]
indent [indents] = [[${convertIndentationToBlockNumber (indents)}]]
indentChar [c] = [[${c}]]
indentDoubleSpace [cc] = [[.]]
toEOL [c] = [[${c}]]
newline [c] = [[${c}]] 
spc [c] = [[${c}]]
```

Reading (in order of simplicity):
4. The rule _indentChar_ gets one matched character from the pattern matcher and returns it
5. The rule _indentDoubleSpace_ gets two matched space characters from the pattern matcher, ignores them and returns a single "." character.
6. The rule _toEOL_  gets one matched character from the pattern matcher and returns it.
7. The rule _newline_  gets one matched character from the pattern matcher and returns it.
8. The rule _spc_  gets one matched character from the pattern matcher and returns it.
3. The rule _indent_ gets one match (called indents) from the pattern matcher and returns a number calculated by the function "convertIndentationToBlockNumber".
2. The rule _line_ gets 4 match captures, each from a compound match (?, *, +) an rearranges them while calling support functions "emitopenbrace()", "emitclosebrace()", "spaces()" and "shiftBlock()".
1. The rule _main_ gets one `+` parameter (called lines) from the pattern matcher and rearranges the output as: a call to the external function _resetBlock_, then uses JS back-tick syntax to create a string consisting of the lines and the result from calling the external function emitclosebrace.  External functions are not built into the tool - they are supplied by the programmer (in this case, I've put the support functions in a file call "support.js").
## The Workbench
The workbench is a simple HTML file that contains a textarea for all 3 input files (source, pattern (grammar), outputter (semantics)) and 1 textarea for the result.

The "generate" button calls the JS function "generate()" which simply reads the textareas and calls the "transpiler()" function.

## Transpiler()

The "transpiler()" function is, itself, quite simple. It
1. Builds a transpiler (using Ohm-JS and Glue)
2. Invokes the transpiler on the input source
3. Outputs the result into the textarea called "transpiled". Outputs some information into the field called "status".

# Result
Below, I've included the result of invoking the SCN Workbench on the above indented code example.

Note that this result contains superfluous blank lines. Our machine will skip over these blank lines, so, they only matter in terms of human-readability. 

Likewise, the formatting might be wrong in places. This doesn't affect machine-readability.

Is it worth the time to get rid of the blank lines and fixing formatting? It depends...

```
getter (rid)
 {
 result <= c.ns[name]
  {
  where deconstruct rid => (_, ns, name)
  synonym c, component
  where component = @ea (rid)

 }
}
setter (rid val)
 {
 c.ns[name] <= val
  {
  where deconstruct rid => (_, ns, name)
  synonym ns, namespace, "namespace within component"
  synonym c, component
  where component = @ea (rid)
  design rule "must not already have a value"

 }
}
def (rid)
 {
 @define all paths (rid)
 where
  {
  define all paths (rid)
   {
   ea (rid)

   }
}
}
where
 {
 ea (rid)
  {
  ea-raw (rid) | design rule "must be a component" => result

  }
 ea-raw (rid)
  {
  typecase (rid.path)
  case string
   {
   lookup (rid.path) => result
   design rule (result) "must not be empty"

    }
  case _
   {
   @getter (ref) => child
   child.static => result

    }
}
 before 
  {
  where ref = rid.path
  synonym ref, component-reference, "recursive reference to a component"
  design rule (ref) "must contain a component namespace reference"

 }
}
design rules
 {
 rid must contain a component namespace reference (rid)
  {
  "c" === rid.ns

  }
 must be a component
  {
  typeof (in) === "component"

  }
 must not already have a value
  {
  component.ns[name] === no-value

 }
}

```
## Github


[Glue Tool](https://guitarvydas.github.io/2021/04/11/Glue-Tool.html)
[Glue Manual](https://guitarvydas.github.io/2021/03/24/Glue-Manual.html)
[Blog](https://guitarvydas.github.io)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
