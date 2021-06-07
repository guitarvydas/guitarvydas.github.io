---
layout: post
title:  "Namespaces"
---

Each component has a _namespace_ which is distinct from the namespaces in other components.

Component naming is relative - there is no "global" namespace.

For emphasis, I break namespaces into 5 sub-categories:
- /i for inputs
- /o for outputs
- /x for connections
- /c for components (child components)
- /n for all other names.

I choose to emphasize that the input namespace is distinct from the output namespace in all components.

Likewise, /x and /c are distinct namespaces.

Input names and output names can appear to be the same, but do not cause name-clashes (because they are in separate namespaces).

I, arbitrarily, choose the following syntax:
- a namespace reference consists of two parts - (1) the component and (2) the namespace within the comonent
- a name reference consists of ":" followed by the name.

For example:
```
comp/i:a
```

refers to the "a" input port of the component "comp".

Further examples:
- comp/o:a - "a" output port of component "comp"
- comp/x:1 - A connection within the component "comp".  We _gensym_ the name of the connection to be "1". The user doesn't actually care.
- comp/c:sub - The component "sub" in the namespace "c" of component "comp".
- comp/n:xyz - The symbol "xyz" in the namespace "n" of component "comp".

# Optimization and Hiding
Later, we might wish to adopt a UNIX-like naming scheme where all parts of a path use the "/" operator.

For example, we might want to rewrite:
```
comp/c:sub/i:a
```
to look like:
```
comp/c/sub/i/a
```

but, that is a syntactical bauble that can be applied later[^syntax].

[^syntax]:Syntax is cheap.

For now, for clarity, I will use the form: `comp/c:sub/i:a`.

# Abbreviating ./

I will use the abbreviation `.` to mean the _current component_.

For example `./i:a` means `comp/i:a` when it appears inside of the component "comp".

This is purely meant for human consumption - writability and readability.

Automation will transform:
```
root comp
./i:a
```
into
```
root comp
comp/i:a
```

# See Also

[References](https://guitarvydas.github.io/2021/01/14/References.html)
[Table of Contents](https://guitarvydas.github.io/2021/05/14/Table-Of-Contents.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
