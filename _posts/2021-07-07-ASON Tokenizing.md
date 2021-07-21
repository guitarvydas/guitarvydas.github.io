---
layout: post
title:  "ASON: Tokenizing"
---
ASON contains many different datatypes.

To parse ASON, I suggest:
1. Convert the input to basic tokens
2. Filter the tokens in layers to produce more-detailed tokens.

# Simple Example
Let's begin with a painfully simple example:
```
    name: "John Smith"
```

This example contains:
1. some leading whitespace
2. an ident ("name")
3. a colon (":")
4. more whitespace
5. a string ("John Smith")
6. a newline (whitespace).

I suggest creating a separate token for each of the above.

# Tokens For Simple Example
Below, is the output from a first-pass tokenizer:
```
W %2520%2520%2520%2520
N name
D: :
W %2520
S %22John%252520Smith%22
W %250A
```

[_Note that this is only the way I chose to do this - there might be many possible solutions to this tokenizing problem_]

Each token appears on a separate line.

Whitespaces, in lines, are ignored (but act as separators).

I've encoded the token "kind" as the first letter on a line.

I've encoded all non-printables in URI format (using JavaScript's `encodeURIComponent()`). Notably, strings don't include the quotes ('"').

Tokens are meant to be _machine-readable_. Human-readability is not of concern at this point in the design. [_Aside: actually, I use an ASCII encoding, to help with debug-ability._]

Tokens are fully described by their code. Each token carries its originating _text_ following the whitespace. This text can be ignored by subsequent filters, but might be useful during the final filter in the chain, which, presumably outputs the token in some more-readable format.

_Some_ tokens include a sub-kind, encoded as a second letter. In the above, there is one example of a token with a sub-kind, the "colon" token `D: ...` [_Aside: in this case, the text is redundant and contains a single colon - this can be optimized-away at a later date (or, more likely, just left alone, since the optimization will probably not have a significant effect on performance on modern hardware)._]

# Filters

After tokenizing, filters can be built in layers. I won't show this at the moment and will discuss details in future essays.

## Filter Example (Simple)
To give a flavor for what filtering might accomplish, examine the above lines 2 and 3.  

We see an ident token followed by a colon.

In ASON, this is written as:
```
name:
```
and, in ASON, this signifies a _setter_, or a "define word".

A filter might collapse those two tokens (lines 2 & 3 in the above list) down into one token, for example
```
e! name
```
resulting in only 5 tokens:
1. some leading whitespace
2. a defineword ("name")
3. more whitespace
4. a string ("John Smith")
5. a newline (whitespace).

Ideally, we will reduce the number of tokens at each stage of filtering.

One of the first filters will be a whitespace-remover.

## Filter Stages - Ordering

Assigning an order to the filters is somewhat tricky and I will defer discussion of this issue for later.

As an example of the kind of trickiness that needs to be handled, consider the issue of strings.

Strings might contain things that look like other kinds of tokens, for example, a string might contain an email address.

It would be wrong to convert email addresses into tokens if those email addresses are embedded in strings.

In the token+filter approach, this problem can easily be solved by filtering strings into tokens before filtering email addresses into tokens.

For example:
```
  name: "John Smith johnsmith@altscript.com"
  email: johnsmith@altscript.com
```
Should become the token stream:
```
W %2520%2520
N name
D: :
W %2520
S %22John%252520Smith%252520johnsmith%252540altscript.com%22
W %250A%2520%2520
N email
D: :
W %2520
N johnsmith
D@ @
N altscript
D. .
N com
W %250A
```

and then collapsed into:
```
G defineWord name
S %22John%252520Smith%252520johnsmith%252540altscript.com%22
g defineWord
G defineWord email
d@ johnsmith altscript.com
```
Don't worry about the unfamiliar token kinds - they will be discussed elsewhere. The thing to notice is that the string is just a string token ("S") and contains something that looks like an email address, whereas the email datatype is filtered into a "d@" token.

# See Also

[ASON](https://altscript.com)
[Blog](https://guitarvydas.github.io)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
