---
layout: post
title:  "SCN Development for ZodeTrip"
---
# Initial Grammar
```
zodeSCN{
  main = room+
  room = "room:" ws* id ws+ statement+ ";room"
  statement = widthStatement | heightStatement | tilesStatement | enterStatement
  widthStatement = "width" ws+ number eol
  heightStatement = "height" ws+ number eol
  tilesStatement = "tiles" ws* "(" numberList ")" eol
  enterStatement = "enter:" ws* tellStatement ";enter" eol
  tellStatement = "tell" ws+ string eol

  numberList = (number ws*)+
  number = negativeNumber | positiveNumber
  negativeNumber = "-" smallinteger
  positiveNumber = smallinteger

  smallinteger = dig+
  dig = "0" .."9"
  ws = " " | "\t" | "\n"
  id = firstIDChar followIDChar*
  firstIDChar = "a" .. "z" | "A" .. "Z"
  followIDChar = "0" .. "9" | firstIDChar
  string = quote notQuote* quote
  quote = "\""
  notQuote = ~quote any
  eol = ws+
}

```

## Ohm-JS vs Other PEG Libraries

Ohm-JS rule names are case-sensitive.

In Ohm-JS, lower-case rule names work just like other PEGs (modulo minor syntactic differences).

In Ohm-JS, upper-case rule names skip `space`s, so most of the `ws` stuff above could go away.

The other big difference between Ohm-JS and other PEG libraries is how matches are tagged.  I will explain this later.  Let's just work on the grammar first.

# Initial Test Code

```
room: default
  width 3
  height 3
  tiles (-1 -1 -1  -1 -1 -1  -1 -1 -1)
  enter:
     tell "Something BAD happened.\nPlease report this bug!\nTHNX 1.0E6!!!"
  ;enter
;room
```

# Ohm Editor




# <img src="https://github.com/guitarvydas/guitarvydas.github.io/blob/master/assets/Ohm%20Editor%20for%20ZodeTrip%20Screen%20Shot%202021-09-02%20at%208.09.14%20AM.png?raw=true" alt="Ohm Editor for ZodeTrip Screen Shot 2021-09-02 at 8.09.14 AM.png" style="zoom:67%;" />See Also

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
