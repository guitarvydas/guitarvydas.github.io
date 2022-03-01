## Introduction

I'm trying to parse Tunney's blog post about [Binary Lambda Calculus](https://justine.lol/lambda/) down to the bit level.

I've captured my thoughts in this blog.  These are notes-to-self.  My current understanding is not-yet-complete, but HTH...

The notes might contain errors in understanding, but that's OK with me, since my understanding grows through iteration...

## Notes

- 2 types
	1. opcodes
	2. references to variables on the stack

2 types needs 1 bit ; 0 => opcode, 1 => ref

2. refs are formally called "De Bruijn Indices", but they are nothing more than anonymous variables.  Forth does this, too, but (2) Curries functions down to 1 parameter (always), Forth allows more than 1 parameter

Opcodes: there are only 2 opcodes, 1 more bit is required ('0' to signify opcode, 0/1 to signify which opcode)
1. "Abstraction" (1st class function of exactly 1 parameter), push the function onto the stack. '00'
2. "Application" Apply a 1st-class function to an arg.  Arg is top-of-stack, 1st class function is at TOS+1 (2nd item on stack). '01'

Ref always begins with a '1' bit, then followed by N 1's, followed by a '0' bit terminator, e.g.

0th item (TOS[^1]) is '10'
Next item (TOS+1) is '110'
TOS+2 item is '1110'
etc.

[^1]: TOS means Top Of Stack.

'(lambda (x) x)' is encoded as ''0010"  which means 
- Abstraction '00'
- TOS ref '10'

The whole function '(lambda (x) x)' needs 4 bits (half a byte).

In JavaScript syntax, `(lambda (x) x)` would be written as 
```
function (x) { return x; }
```

The *program* '((lambda (x) x) 0101)' requires 8 bits (a full byte).  0101 is arbitrary, it gets pushed into meory and passed as the 1st (only) arg to the function '(lambda (x) x)' - which returns its arg whatever it is, in this case '0101'.

In JavaScript, the program syntax is
```
((function (x) {return x;}) 0)
```

The whole program is 1 byte long - 00100101 binary.

Stdin works with characters (8 bits) not single bits.  So, the shell script:
`printf 0010 ; printf 0101`
outputs 8 *characters* (a total of 64 bits).  7 bits in each character are wasted and the blc parser discards those bits and only uses the bottom-most bit.  (N.B. the command-line version of *printf* does not add a terminating '\0' like C does.)

In ASCII, 
- the character '0' is represented by the code 0x30, which is binary ?1100000, and,
- the character '1' is 0x31, which is binary ?1100001.
(where "?" is the parity bit ; ASCII is actually 7 bits plus 1 parity bit)
(I'm leaving the parity bit as ? to avoid even more confusion[^2])

[^2]: Parity is calculated by the hardware by simply summing all of the bits in the byte (except the parity bit).  If the sum is even, the parity bit is set to 0, else if the sum is odd, the parity bit is set to 1.  There are no other possibilities.  An even binary number *always* ends with a 0 bit, an odd binary number *always* ends with a 1 bit.  This kind of summing discards all carries and the result is always a single bit. (IOW, it uses a 1-bit register and ignores overflow).

The parser discards the top 7 bits.  We get only the bottom-most bit (the LSB):
- '0' -> binary 0
- '1' -> binary 1

(This works due to the definition of ASCII.  Essentially, this is a clever hack.  It is an idiom in assembler circles).

The character string 0010 is 0x30303130 in hex, which is 
```
?1100000?1100000?1100001?1100000
```
in binary.

The *character* string 0010 is parsed from 32 *bits* down to 4 *bits*, binary 0010.

The parser reads characters from stdin, strips them down and puts them into memory (an array).

Church numeral 0 is *defined* to be the unity function (lambda (x) x).

"False" is *defined* to be the same as Church numeral 0.

