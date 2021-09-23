---
layout: post
title:  "Agile Takeaways"
---
# Goal of Agile
The goal of Agile is to deal with the uncertainty of the Design process.

Agile deals with design uncertainty by involving the stake holder(s) multiple times during the design process.

Most customers, stake-holders, cannot specify Requirements with enough grueling detail to allow implementation.  Most customers, stake-holders, do not _want_ to deal with _all_ of the details.

Agile is just a stop-gap measure applied to Design, until we find a better way to perform Design with less uncertainty.

# Religion of Agile
Agile has become dogmatic - a religion.

Many programmers focus on the _rituals_ of Agile, without addressing the _goals_ of Agile.
# Takeaways from Agile
- Stake-holders cannot (will not) specify _all_ of the details of a problem.
# Anti-Takeways from Agile
## Sprints Are Too Long
 2/3-week sprints are too long.

 We should be striving for continuous improvement in the process of gathering requirements.
### 2 Hour Sprints 
 We should be striving for 2-hour sprints.
### Redefining Sprints
 We should be striving to change the concept of sprints into something even more productive.
# Flexibility
We want:
- flexibility in the Design
- optimal behavior in the field.

This suggests that we should break programming down into two major categories:
1. Flexible Design
2. Optimization for Delivery.

The categories have different goals.

We should treat each category differently.

We should not conflate both categories into the same activity, nor the same PL[^pl].

[^pl]: PL means Programming Language

## Inflexibility
Optimization removes flexibility to achieve better performance.

Premature optimization is pervasive, yet hidden, in most apps written with current PLs.

## Tell: Choosing Programming Language First
Choosing a PL before fully understanding a problem leads to later inflexibility.

The only "good" reason to hire programmers experienced in a certain language is to maintain and upgrade existing code.
## Tell: Choosing Only One Programming Language
If the programming language does not fit the problem, aspects of the problem-solution must be force-fit into the programming language, e.g. Relational Programming languages do not fit output formattting (well).

The use of only one programming language is a _tell_.  

All aspects of the solution might not suit themselves to a single, chosen language.

(Sometimes, all aspects of the solution do fit a given language. This is an exception, not the rule).

The use of a single programming language - for design - is indicative of the "programmers are interchangeable" mind-set, instead of the "best-of" mind-set. For example, Apple Computers lets the cost of their computers be determined by a "best-of features" mind-set, instead of allowing cost to drive which features are included.

Note that I argue that PLs are cheap to build[^cheap], today.

[^cheap]:"Cheap to build" means hours, not years, for implementation.

## Indirection
Indirection retains flexibility at the expense of optimization.
## Multiple Syntaxes
Designs often have multiple facets.

Each facet might be best expressed in a different syntax.

Hence, an app should employ multiple syntaxes.

[I argue that SCNs - Solution Centric Notations - should be used. SCNs are cheap to build (hours instead of years).  Multiple SCNs can be tuned for a specific problem.  SCNs are so cheap, that one can build SCNs for a specific _problem_ instead of resorting to one off-the-shelf PL].

## Diagrammatic Syntaxes
There is no reason to use only text-based notations for a given problem.

Diagrams can be transpiled to executable code. I detail how to do this in other essays.

Architects' toolbelts[^paradigms] should include many textual and diagrammatic PLs.

[^paradigms]: Paradigms are more important than syntax
## Whiteboards
Most stake-holders and most CTOs use whiteboards to present their ideas to implementors.

Q: Can we capture the whiteboard drawings?

A: Yes, using photos and drawing editors.

Q: Can we manually transpile drawings into working code?

A: Yes, I document how to do this in other essays.

Q: Can we automatically transpile drawings into working code? (I.E. can we build compilers for diagrammatic languages?)

A: Yes, I document how to do this in other essays[^modern].

[^modern]: Modern hardware can run exhaustive-search languages, e.g. PROLOG and Relational Programming, which makes transpiling diagrams-to-code simple.

# Reuse In The Large
It is not enough to reuse code.

It is not enough to reuse Architecture.

We should reuse organizational principles from other professions.

For example, Architecture/Engineering/Construction organizational structure could be borrowed from the construction industry.

Most software organizations don't yet understand that Engineering is not Coding.

# Code is cheap.

Code is cheap.

Thinking is hard.

# Software Development Roles
See [Software Development Roles](https://guitarvydas.github.io/2020/12/10/Software-Development-Roles.html).

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
