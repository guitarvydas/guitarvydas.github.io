---
layout: post
title:  "Code Markdown to Bash"
---

# Introduction

A very, very simple transpiler from code-markdown to bash.

Transpile
```
# _containment_

## _fb pipeline_
	script1
	script2
	script3



## _details_
### script1
	echo hello
	echo world 
	echo from script 1
### script2
	echo hello
	echo world 
	echo from script 2
### script3
	echo hello
	echo world 
	echo from script 3
```
to
```
#!/bin/bash
# _containment_

clear
set -e
trap 'catch' ERR

catch () {
    echo '*** FATAL ERROR ***'
    exit 1
}

# _details_
script1 () {
	echo hello
	echo world 
	echo from script 1

}
script2 () {
	echo hello
	echo world 
	echo from script 2

}
script3 () {
	echo hello
	echo world 
	echo from script 3

}

# _fb pipeline_
	script1
	script2
	script3
```

## Preamble
The preamble traps errors and prints a FATAL
```

clear
set -e
trap 'catch' ERR

catch () {
    echo '*** FATAL ERROR ***'
    exit 1
}
``
Any sub-script that exits with a non-0 exit code, will be caught by the above.

# Why?
## Layers - Important Stuff At The Top
We _want_ to build software in layers.

We _want_ the important stuff to be at the top of the script file, but, declaration-before-use requires that we define the details first and put the important stuff at the bottom of the script.

We _want_ to use md-mode to elide details, so that we can look at the script in layers. We press `TAB` to expand layers only if we want to see the details.

We consider variables, traps, etc. to be at lower layers.

We _want_ the transpiler to transpile our .md script into valid _bash_ code.

This is an examplar - we show how to build a simple transpiler. We hope that the reader can build further transpilers that have more layers than what we show.

This is an examplar - we show some of the intermediate steps:
1. Convert md to structured pseudo-code (braces) [md2pseudo](https://guitarvydas.github.io/2021/08/03/Code-Markdown-to-Structured-Pseudo-code.html)
2. Convert the pseudo-code to bash-like code [md 2 bash](https://github.com/guitarvydas/md2bash)
3. Insert swipl stuff (in a later essay).

Also, we show how easy it is to flip parsed code at will [flip](https://guitarvydas.github.io/2021/08/03/Flipping-Code.html).

## Emacs md-mode
Note that the above input syntax is editable by emacs md-mode.

Emacs md-mode provides the `TAB` key to allow eliding layers.


# Usage and Testing

1. Load md2bash.html into a browser.
2. Scroll all the way down to the bottom and press `generate`.
3. Copy the resulting code from the bottom textarea ("transpiled to bash"), and paste it into a file `test.bash`.
4. chmod a+x test.bash
5. ./test.bash

# Github

[md2bash](https://github.com/guitarvydas/md2bash)

# See also

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
