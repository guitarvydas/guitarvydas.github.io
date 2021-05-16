# Arithmetic Example for WASM Using Ohm-JS and Glue

## Introduction
In this essay, I discuss how to build a WASM transpiler that converts simple notation[^2] for arithmetic into WASM code, and runs the result.

The transpiler technology is meant to be simple and to make you yawn.

[^2]: I use the word _notation_ to mean a light-weight programming language (lighter weight than even a DSL).
## Code - Grammar and Rewrite Specifications
The full Grammar and the Rewrite specifications (`glue` code) can be found in the Appendices.

A full specification for a transpiler consists of
- a grammar (in Ohm-JS style)
- a rewrite specification (in `glue` style).

More details can be found in the Appendices.

The following discussion is meant to be a gentle introduction to this transpiler technology.  (Yawn).

## Grammar Rules
Let's look at the AddExpr rule..

```
  AddExp
    = AddExp "+" MulExp  -- plus
    | AddExp "-" MulExp  -- minus
    | MulExp
```


`AddExp` says:
- Try to match an `AddExp` followed by a `+` followed by a `MulExp`.  
- If that fails, try `AddExp` followed by `-` followed by a `MulExp`.  
- If that fails, try a `MulExp`.

### PDFAs
This demonstrates the main difference between PEG `grammars` and `REGEXs`.

PEG (and other parser-generators) allow the programmer to write subroutines that contains sub-matches.  The subroutines can be called as often as needed and, they can be called recursively.

For example, looking only at the `AddExp` rule, we don't need to know what the sub-rule `MulExp` is.  We just use `MulExp`.  At the `AddExp` layer, the sub-rule `MulExp` is matched as a single item.  The single match maps directly to a single parameter in the follow-on, _semantics_, code.  

Technically, the difference is that PEG (and all parsers, in general) uses a stack, whereas REGEX does not employ a stack (jargon: parsers use push-down-finite-automata vs. discrete-finite-automata, resp.  The issue is whether the Stack is exposed to the programmer, not whether the technologies use stacks in their implementations).

The specification for a PEG parser usually needs more than one line of code, but most of the code is understandable vs. being a single string of hieroglyphics.

### Left Recursion
The `AddExp` example also shows that `left recursion` is supported by Ohm-JS.  

[This is a technical point that improves readability.  If you can read and understand the above grammar, then you don't need to go down the rabbit hole of understanding what 'left recursion` is all about.]

### Rule Splitting
The `AddExp` rule is transpiled, by Ohm-JS into three rules: 
- AddExp_plus
- AddExp_minus
- AddExp

The programmer is responsible to creating the splits[^3].

[^3]: If you don't like this, just write a preprocessor (as a PEG grammar).

The first two lines of the rule
```
    = AddExp "+" MulExp  -- plus
    | AddExp "-" MulExp  -- minus
```
match 3 items each
1. an AddExp
2. a "+" or "-"
3. a MulExp

while the last line matches only 1 item
```
    | MulExp
```
1. a MulExp

The symbols following the `--` in the first two lines become suffixes to the rule name, e.g. `AddExp_plus` and `AddExp_minus`.

A PEG grammar can _match_ different numbers of items.  The grammar calls follow-on code (called the _semantics_) as functions for every rule and passes the matched items in as parameters. 

Ohm-JS checks that the generated _semantics_ functions have consistent parameter lists, so the AddExp rule needs to be broken (by the programmer) into separate rules, using `--` name-mangling.

[Other PEG libraries use a different strategy - e.g. the programmer must embed sub-rule names into the grammar, which allows the generator to create single functions for each rule that use programmer-supplied parameter names.  The Ohm-JS strategy puts more onus on the code generator, but keeps the grammar intact and readable.  I prefer the Ohm-JS strategy, as it leads to better separation between grammar and semantics.]

### Reading the Grammar
To read - and understand - the grammar, start at the top-most rule, call `Top` (in this case).

It says: 
1. At the top level, match an Expression (`Exp`).
2. To match an Expression, match an `AddExp`.
3. To match an `AddExp` 
- try to match an `AddExp_plus`, 
- then try to match `AddExp_minus`, 
- then try to match `MulExp`.  

In PEG, matching order matters[^4].  

[^4]: The programmer is responsible to order rules in the correct sequence (usually longest to shortest).  Other parser technologies, e.g. parsers based on CFG theory, don't need programmer-specified rule ordering, but, those technologies put limits on what _can_ be matched.  PEG usually wins (from the perspective of practicality).  PEG can match patterns that CFG parsers (like YACC) can't match. [The "classic" example is that PEG can match balanced parentheses, whereas CFGs can't.  The real test is whether PEG grammars can be easily written for everyday cases.  I believe that PEG is readable, that programmer-supplied rule-ordering is easy to specify, and, is "natural" for programmers to write.  IMO, PEG is the next REGEX.  Ohm-JS is the best PEG variant I've used.].

The `MulExp` rule is similar to the `AddExp` rule.

The `PriExp` rule matches for a "primary".  

First, `PriExp` tries to match a parenthesized expression.  If an open parenthesis found, then we start at the top again and try to match an `Exp`.

The idea of writing a grammar is to specify the pattern-matching in _layers_.  The layers can recur (loop back to the top) as needed.  In this case, we loop back to the top if we begin to see a parenthesized expression.  Note that a parenthesized expression can contain another parenthesized expression - the grammar will handle it recursively (to the limits of our computer's memory).  

This example grammar will "bookmark" a sub-match and re-start at the top[^5] when it hits `PriExp_paren`.

[^5]: Actually, it restarts at `Exp` which is almost-the-top.

PEG does its matching with bookmarks and backtracking.  If one path through the grammar fails, it will try another one.  If all paths fail, the transpiler throws up its hands and declares a non-match (aka "syntax error").

### Rule Descriptions
In `ident  (an identifier)` and `number  (a number)`, we see another feature of Ohm-JS - the ability to tag a rule with an informative string (in parentheses) that is included in the error message, when the match fails.

### + * and ?
The rules `ident` and `number` also contain `*` and `+` operators.  These work similarly to REGEX.

See the Appendix for Ohm-JS documentation.

## Semantics (Glue)
Ohm-JS expects programmers to write follow-on code in JavaScript.

We can use Ohm-JS to write a simple tool that writes JavaScript for us.  I call this tool `glue`.

In the example below, we use the grammar to generate a JS app (a pattern-matcher) that accepts pseudo-code and produces WASM code.

`Glue` doesn't do very much - it parses input code and then creates output code.

For parsing, `glue` uses Ohm-JS.  For outputting, `glue` uses JavaScript back-tick syntax[^6].

[^6]: Back-tick strings are called _template strings_ in JS and EcmaScript.

It may, at first, seem surprising that we can create WASM code by just using JS back-tick syntax.

The _trick_ is to do things in a very repeatable (aka boring) manner.

Ohm-JS plays into this _trick_, easily.  (`Glue` could do more, and might do more in the future, but this quick-and-dirty trick is enough to generate WASM.  Why add complexity when simplicity will suffice?).

Let's begin by looking at the code associated with the `AddExp` grammar rule, above.
```
  Exp [e] = [[${e}]]
```
This is the simplest form of `glue` rule.

It consists of
- a name, `Exp`
- a list of parameters, `[e]`
- a separator `=`
- a rewrite rule, `[[${e}]]`.

The `glue` rule `name` must correspond - exactly - to the name of a grammar rule.  There needs to be exactly one `glue` rule for each grammar rule.

The parameters consist of programmer-chosen names, separated by spaces.  

There must be one parameter for each sub-match in a rule. 

The names are Javascript compatible and are resolved and used in the rewrite portion.  

A parameter name can be prefixed by the `@` operator (not present in `Exp`), to mean that the parameter lines up with a tree of sub-matches, i.e. generated by a grammar sub-match that has `*`, `+` or `?` suffixes.  

Parameter names are used in the rewrite portion without the `@` prefix. [The `@` is a signal to `glue` to unpack the tree sub-match in a recursive manner - see `Ohm-JS` documentation.]

The rewrite is a literal string contained in double-brackets, `[[ ... ]]`.  The literal string is a JavaScript back-tick string.  In this kind of string, `${...}` is used to refer to parameters.  [Aside - `glue` simply wraps the string in back-ticks and generates a JavaScript string.  Leading spaces are skipped.  Yawn.]

In summary,
```
  Exp [e] = [[${e}]]
```
means:
- line up with the grammar rule `Exp`
- supply the grammar sub-match in the named parameter `e`
- rewrite the sub-match as the JavaScript string `\`${e}\``
- return the JavaScript string from the rule (to the calling layer).

The `ident` rule uses an `@` parameter.
```
ident [l @a] = [[local.get \$${l}${a}]]
```
This rule matches up with the `ident` rule in the grammar:
```
ident  (an identifier)
    = letter alnum*
```
where `alnum*` uses the `*` operator.

In the `glue` rule
- we use the named parameter `l` to hold from the sub-match `letter` 
- and we use the named parameter `alnum` to hold the tree from the sub-match `alnum*`.

[Note that the grammar rule also contains a rule description `(an identifier)` which is ignored in the `glue` rule.]

The `glue` rewrite is `[[local.get \$${l}${a}]]` which returns the JavaScript string `\`local.get \$${l}${a}\``.  This rewrite creates a string that contains the literal characters `local.get $` followed by the values of the parameters `l` and `a`.  

`Glue` unpacks the sub-matches from the grammar, resulting in the `l` being bound to the sub-match from `letter` and `a` being bound to the sub-match from `alnum*`.  The sub-match from `alnum*` is treated specially by `glue`[&7].

[^7]: `glue` returns _all_ of the match as a single string joined together (by Javascript's .join('') operation)).

The `Top` rule uses `glue`s preamble feature.

The RHS (right-hand side) of the `glue` rule contains an arbitrary block of Javascript code contained in double-braces `{{ ... }}`.  The preamble is executed before any of the parameters are unpacked[^8].

[^8]: This can require knowledge of the simple name-mangling rules of `glue`.  The best way to understand the name-mangling operations is to examine the code generated by `glue`.  Same as before: if you don't like this, feel free to write a PEG-based preprocessor (chain preprocessors in a pipeline, the more the merrier).  I believe in YAGNI - this set of rules and quirks is enough to get my job done.  N.B. you don't need to understand name-mangling to use scope variables (see below).

In the end, `glue` generates a Javascript program.  The Javascript program is a transpiler - a parser and a code-generator.  The program is run using `node` with input from a file-to-be-parsed.

The `grasem` tool joins the Ohm-JS grammar with a corresponding `glue` specification and produces one Javascript parser program from the pair.

### RY
In the set of `arithmetic` examples, we produce code for 4 languages using one Ohm-JS grammar.  

At present, we simply clone the `grasem` template 4 times.

Ohm allows multiple follow-on (_semantics_) functions for one grammar, but `glue` does not use this feature, at the moment.  A simple project would be to extend `glue` to allow multiple rewrites for any one grammar (collapsing the `arithmetic` examples from 4 files into 1 file).  The project would be written in `glue` and shell scripts (`/bin/*sh`).  Another approach would be to use the `m4` macro processor to provide `include` operations - in fact, this can be done immediately, without writing any new code. [M4 makes the above project moot.  Instead of extending `glue`, just use `M4` or `cat`, or, ...].
### Design of the Grammar+Rewrites
The Ohm-JS grammar for the simple `arithmetic` language simply creates a CST (concrete syntax tree of the actual input, similar to an AST) and then walks the tree using the specified rewrite strings.

The topmost rule `Top` outputs the resulting string wrapped in appropriate WAT details.  [WAT is the human-readable, text, version of a WASM file.  See `wasrun.bash` for how to convert a WAT file into a WASM file.]

The bottom-most rules - `ident`, `number_fract` and `number_whole` create WASM code to push the operand onto the WASM stack (`f64.const` to push a double-float constant onto the WASM stack and `local.get` to push a named WASM parameter onto the WASM stack.).

The rest of the layers - `glue` rules - simply rearrange the operand and WASM operators.  

For example, the rule `AddExp_plus` is:
```
  AddExp_plus [e1 op e2] = [[${e1}\n${e2}\nf64.add\n]]
```

This rule takes 3 operands - two expressions and one operator.  The rewrite rearranges the operands in RPN[^1] order and suffixes the string with `f64.add` (and appropriate newlines `\n`).

[^1]: RPN means _Reverse Polish Notation_.

### The ident Rule
The `ident` rule is implemented only in the WASM transpiler.  The other tranpsilers - pymath, jsmath and lispmath - do not deal with this rule.
### Exponentiation
Exponentiation - the `ExpExp_power` rule - is not, presently implemented in the WASM transpiler.  Finishing this rule consists of looking up the exponentiation operator in the WASM instruction manual and writing the rewrite rule.  This is left as an exercise for the reader.
### Foreign Functions
As can be seen in wasmrun.bash, we expect a file `foreign.js` to exist.  It is meant to contain support functions needed for a specific transpiler.

In this simple example, there are no support functions, so the file is empty.

### Scope Variables
`Glue` also supports the creation and querying of variables tied to the CST tree-walk.  See the [Glue Manual](https://guitarvydas.github.io/2021/04/11/Glue-Tool.html).

This simple example does not use scope variables.



## Appendix - Arithmetic Grammar
The grammar for arithmetic is lifted, literally, from [Ohm Arithmetic Example](https://github.com/harc/ohm/tree/master/examples/math)

```
Arithmetic {
  /* WASM code emitter */
  
  Top = Exp
  
  Exp
    = AddExp

  AddExp
    = AddExp "+" MulExp  -- plus
    | AddExp "-" MulExp  -- minus
    | MulExp

  MulExp
    = MulExp "*" ExpExp  -- times
    | MulExp "/" ExpExp  -- divide
    | ExpExp

  ExpExp
    = PriExp "^" ExpExp  -- power
    | PriExp

  PriExp
    = "(" Exp ")"  -- paren
    | "+" PriExp   -- pos
    | "-" PriExp   -- neg
    | ident
    | number

  ident  (an identifier)
    = letter alnum*

  number  (a number)
    = digit* "." digit+  -- fract
    | digit+             -- whole
}
```

## Appendix - Glue Specification for WASM Arithmetic

```
  Top [e] = 
{{ 
   console.log ("(module"));
   console.log ( " (func $custom (param $x f64) (param $y f64) (result f64)" );
}}
[[
${e})
  (export "custom" (func $custom))
)
    ]]
  Exp [e] = [[${e}]]
  AddExp_plus [e1 op e2] = [[${e1}\n${e2}\nf64.add\n]]
  AddExp_minus [e1 op e2] = [[${e1}\n${e2}\nf64.sub\n]]
  AddExp [e] = [[${e}]]
  MulExp_times [e1 op e2] = [[${e1}\n${e2}\nf64.mul\n]]
  MulExp_divide [e1 op e2] = [[${e1}\n${e2}\nf64.div\n]]
  MulExp [e] = [[${e}]]
  ExpExp_power[p op e] = [[(???exp ${p} ${e})]]
  ExpExp [p] = [[${p}]]
  PriExp_paren [lp p rp] = [[${p}]]
  PriExp_pos [sign p] = [[${p}]]
  PriExp_neg [sign p] = [[${p}\nf64.neg]]
  PriExp [p] = [[${p}]]
  ident [l @a] = [[local.get \$${l}${a}]]
  number_fract [@numerator dot @denominator] = [[f64.const ${numerator}.${denominator}]]
  number_whole [@n] = [[f64.const ${n}]]
```
## Appendix - Generated JavaScript Transpiler from Arithmetic to WASM
[warts and all...]
```
// npm install ohm-js
'use strict';

const grammar =
      `
Arithmetic {
  /* WASM code emitter */
  
  Top = Exp
  
  Exp
    = AddExp

  AddExp
    = AddExp "+" MulExp  -- plus
    | AddExp "-" MulExp  -- minus
    | MulExp

  MulExp
    = MulExp "*" ExpExp  -- times
    | MulExp "/" ExpExp  -- divide
    | ExpExp

  ExpExp
    = PriExp "^" ExpExp  -- power
    | PriExp

  PriExp
    = "(" Exp ")"  -- paren
    | "+" PriExp   -- pos
    | "-" PriExp   -- neg
    | ident
    | number

  ident  (an identifier)
    = letter alnum*

  number  (a number)
    = digit* "." digit+  -- fract
    | digit+             -- whole
}

  

`;


function ohm_parse (grammar, text) {
    var ohm = require ('ohm-js');
    var parser = ohm.grammar (grammar);
    var cst = parser.match (text);
    if (cst.succeeded ()) {
	return { succeeded: true, message: "OK", parser: parser, cst: cst };
    } else {
	//console.log (parser.trace (text).toString ());
	//throw "glue: Ohm matching failed";
        
        return { succeeded: false, message: cst.message, parser: parser, cst: cst };
    }
}

function getNamedFile (fname) {
    var fs = require ('fs');
    if (fname === undefined || fname === null || fname === "-") {
	return fs.readFileSync (0, 'utf-8');
    } else {
	return fs.readFileSync (fname, 'utf-8');
    }	
}
'use strict'

var _scope;

function scopeStack () {
    this._stack = [];
    this.pushNew = function () {this._stack.push ([])};
    this.pop = function () {this._stack.pop ()};
    this._topIndex = function () {return this._stack.length - 1;};
    this._top = function () { return this._stack[this._topIndex ()]; };
    this.scopeAdd = function (key, val) {
	this._top ().push ({key: key, val: val});
    };
    this._lookup = function (key, a) { 
	return a.find (obj => {return obj && obj.key && (obj.key == key)}); };
    this.scopeGet = function (key) {
	var i = this._topIndex ();
	for (; i >= 0 ; i -= 1) {
	    var obj = this._lookup (key, this._stack [i]);
	    if (obj) {
		return obj.val;
	    };
	};
        console.log ('*** scopeGet error key=' + key + ' ***');
	console.log (this._stack);
	console.log (key);
	throw "scopeGet internal error";
    };
    this.scopeModify = function (key, val) {
	var i = this._topIndex ();
	for (; i >= 0 ; i -= 1) {
	    var obj = this._lookup (key, this._stack [i]);
	    if (obj) {
		obj.val = val;
		return val;
	    };
	};
        console.log ('*** scopeModify error key=' + key + ' ***');
	console.log (this._stack);
	console.log (key);
	throw "scopeModify internal error";
    };
}

function scopeAdd (key, val) {
    return _scope.scopeAdd (key, val);
}

function scopeModify (key, val) {
    return _scope.scopeModify (key, val);
}

function scopeGet (key, val) {
    return _scope.scopeGet (key, val);
}

function _ruleInit () {
    _scope = new scopeStack ();
}

function _ruleEnter (ruleName) {
    _scope.pushNew ();
}

function _ruleExit (ruleName) {
    _scope.pop ();
}

_ruleInit ();
function addSemantics (sem) {
    sem.addOperation (
	'_glue',
	{
	    Top : function (_e,) {
		_ruleEnter ("Top");
		console.log ("(module"));
		console.log ( " (func $custom (param $x f64) (param $y f64) (result f64)" );

		var e = _e._glue ();
		var _result = `${e})
  (export "custom" (func $custom))
)
    `;
		_ruleExit ("Top");
		return _result;
	    },
	    Exp : function (_e,) {
		_ruleEnter ("Exp");

		var e = _e._glue ();
		var _result = `${e}`;
		_ruleExit ("Exp");
		return _result;
	    },
	    AddExp_plus : function (_e1,_op,_e2,) {
		_ruleEnter ("AddExp_plus");

		var e1 = _e1._glue ();var op = _op._glue ();var e2 = _e2._glue ();
		var _result = `${e1}\n${e2}\nf64.add\n`;
		_ruleExit ("AddExp_plus");
		return _result;
	    },
	    AddExp_minus : function (_e1,_op,_e2,) {
		_ruleEnter ("AddExp_minus");

		var e1 = _e1._glue ();var op = _op._glue ();var e2 = _e2._glue ();
		var _result = `${e1}\n${e2}\nf64.sub\n`;
		_ruleExit ("AddExp_minus");
		return _result;
	    },
	    AddExp : function (_e,) {
		_ruleEnter ("AddExp");

		var e = _e._glue ();
		var _result = `${e}`;
		_ruleExit ("AddExp");
		return _result;
	    },
	    MulExp_times : function (_e1,_op,_e2,) {
		_ruleEnter ("MulExp_times");

		var e1 = _e1._glue ();var op = _op._glue ();var e2 = _e2._glue ();
		var _result = `${e1}\n${e2}\nf64.mul\n`;
		_ruleExit ("MulExp_times");
		return _result;
	    },
	    MulExp_divide : function (_e1,_op,_e2,) {
		_ruleEnter ("MulExp_divide");

		var e1 = _e1._glue ();var op = _op._glue ();var e2 = _e2._glue ();
		var _result = `${e1}\n${e2}\nf64.div\n`;
		_ruleExit ("MulExp_divide");
		return _result;
	    },
	    MulExp : function (_e,) {
		_ruleEnter ("MulExp");

		var e = _e._glue ();
		var _result = `${e}`;
		_ruleExit ("MulExp");
		return _result;
	    },
	    ExpExp_power : function (_p,_op,_e,) {
		_ruleEnter ("ExpExp_power");

		var p = _p._glue ();var op = _op._glue ();var e = _e._glue ();
		var _result = `(???exp ${p} ${e})`;
		_ruleExit ("ExpExp_power");
		return _result;
	    },
	    ExpExp : function (_p,) {
		_ruleEnter ("ExpExp");

		var p = _p._glue ();
		var _result = `${p}`;
		_ruleExit ("ExpExp");
		return _result;
	    },
	    PriExp_paren : function (_lp,_p,_rp,) {
		_ruleEnter ("PriExp_paren");

		var lp = _lp._glue ();var p = _p._glue ();var rp = _rp._glue ();
		var _result = `${p}`;
		_ruleExit ("PriExp_paren");
		return _result;
	    },
	    PriExp_pos : function (_sign,_p,) {
		_ruleEnter ("PriExp_pos");

		var sign = _sign._glue ();var p = _p._glue ();
		var _result = `${p}`;
		_ruleExit ("PriExp_pos");
		return _result;
	    },
	    PriExp_neg : function (_sign,_p,) {
		_ruleEnter ("PriExp_neg");

		var sign = _sign._glue ();var p = _p._glue ();
		var _result = `${p}\nf64.neg`;
		_ruleExit ("PriExp_neg");
		return _result;
	    },
	    PriExp : function (_p,) {
		_ruleEnter ("PriExp");

		var p = _p._glue ();
		var _result = `${p}`;
		_ruleExit ("PriExp");
		return _result;
	    },
	    ident : function (_l,_a
			      ,) {
		_ruleEnter ("ident");

		var l = _l._glue ();var a = _a._glue ().join ('');
		var _result = `local.get \$${l}${a}`;
		_ruleExit ("ident");
		return _result;
	    },
	    number_fract : function (_numerator
				     ,_dot,_denominator
				     ,) {
		_ruleEnter ("number_fract");

		var numerator = _numerator._glue ().join ('');var dot = _dot._glue ();var denominator = _denominator._glue ().join ('');
		var _result = `f64.const ${numerator}.${denominator}`;
		_ruleExit ("number_fract");
		return _result;
	    },
	    number_whole : function (_n
				     ,) {
		_ruleEnter ("number_whole");

		var n = _n._glue ().join ('');
		var _result = `f64.const ${n}`;
		_ruleExit ("number_whole");
		return _result;
	    },

	    _terminal: function () {return this.primitiveValue; }
	});
}


function main () {
    // usage: node glue <file
    // grammar is inserted from grasem.ohm
    // test.grasem is read from stdin
    var text = getNamedFile ("-");
    var { succeeded, message, parser, cst } = ohm_parse (grammar, text);
    var sem = {};
    var outputString = "";
    if (cst.succeeded ()) {
	sem = parser.createSemantics ();
	addSemantics (sem);
	outputString = sem (cst)._glue ();
	return { succeeded: true, message: "OK", cst: cst, semantics: sem, resultString: outputString };
    } else {
	return { succeeded: false, message: message, cst: cst, semantics: sem, resultString: outputString };
    }
}


var { succeeded, message, cst, semantics, resultString } = main ();
if (succeeded) {
    console.log (resultString);
} else {
    process.stderr.write (`${message}\n`);
    return false;
}
```
## Appendix - Bash File to Run the WASM Transpiler (wasmrun.bash)
```
#!/bin/bash
set -e
WTOOLSDIR=/Users/tarvydas/quicklisp/local-projects/wabt/build

../grasem/run.bash wasmmath.grasem >_.js

cat foreign.js _.js >_wasmmath.js
node _wasmmath.js < ex1.math >_temp.wat
${WTOOLSDIR}/wat2wasm _temp.wat -o _temp.wasm
node wasm.js

node _wasmmath.js < ex2.math >_temp.wat
${WTOOLSDIR}/wat2wasm _temp.wat -o _temp.wasm
node wasm.js

node _wasmmath.js < ex4.math >_temp.wat
${WTOOLSDIR}/wat2wasm _temp.wat -o _temp.wasm
node wasm.js

node _wasmmath.js < ex5.math >_temp.wat
${WTOOLSDIR}/wat2wasm _temp.wat -o _temp.wasm
node wasm.js

node _wasmmath.js < ex6.math >_temp.wat
${WTOOLSDIR}/wat2wasm _temp.wat -o _temp.wasm
node wasm.js
```
### Appendix - Wasm.js Support code
```
var fs = require ('fs');

async function getws () {
    var w;
    try {
	w = fs.readFileSync('_temp.wasm');
    } catch (e) {
	console.log ("error: " + e);
    }
    return await WebAssembly.instantiate(w)
}

var w = getws ();
w.then (function (value) {
    console.log (value.instance.exports.custom (3,5));
});
```
(Note that the parameters (3,5) are chosen arbitrarily.  See what happens when you change them.) 
## Appendix - Glue Manual
[Glue Manual](https://guitarvydas.github.io/2021/04/11/Glue-Tool.html)
## Appendix - Grasem Manual
[Grasem Manual](https://guitarvydas.github.io/2021/04/11/Grasem.html)
## Appendix - Ohm-JS
[Ohm-JS](https://github.com/harc/ohm)
## Appendix - Ohm In Small Steps
[Ohm In Small Steps](https://guitarvydas.github.io/2020/12/09/OhmInSmallSteps.html)
 
 This essay - Ohm In Small Steps - also, includes a Scheme-to-JS transpiler that creates a simple PROLOG library in JS, used as a running example.

## Appendix - More About PEG
[My essays](https://guitarvydas.github.io/) are not restricted to PEG.  

If you want only PEG-related opinions, look at the [Table of Contents](https://guitarvydas.github.io/2021/05/14/Table-Of-Contents.html) and look for the PEG sections, and, for the Ohm sections.
## Appendix - Github
[Code](https://github.com/guitarvydas/arithmetic)

N.B. This essay deals with only `wasmmath.grasem`, but the codebase includes transpilers for Python, JS and Lisp.
