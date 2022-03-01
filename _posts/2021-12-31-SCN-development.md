---
layout: post
title:  "SCN Development for ZodeTrip"
---

(unfinished)

# Initial Grammar
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
# Initial Test Code
room: default
  width 3
  height 3
  tiles (-1 -1 -1  -1 -1 -1  -1 -1 -1)
  enter:
     tell "Something BAD happened.\nPlease report this bug!\nTHNX 1.0E6!!!"
  ;enter
;room
# Ohm Editor

# See Also
[References](https://guitarvydas.github.io/2021/01/14/References.html)
[Table of Contents](https://guitarvydas.github.io/2021/12/10/Table-of-Contents-Dec-01-2021.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
