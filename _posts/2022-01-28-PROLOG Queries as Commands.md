---
layout: post
title:  "PROLOG Queries as Commands"
---
junk.pl:
```
#!/usr/bin/env swipl
:- initialization query.

query:-
    consult(user),
    triple(father,paul,F),
    write(user_output,F),
    halt.

```

junkfb.pl:
```
triple(father,john,george).
triple(father,paul,ringo).
```

```
chmod +x junk.pl
./junk.pl <junkfb.pl
```
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
