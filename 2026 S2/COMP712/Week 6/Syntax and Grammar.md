
### EBNF Control forms

Sequence - statement or expression reads left to right 
Choice - either or (similar to regular expressions), left hand side or right hand side
Options - Can be one of many in a square bracket
Repetitions - Repeating 0 one or more times etc

Grammar of EBNF is a set of rules, each rule is of the form of the left hand side (the symbol) or the right hand side (how we define the symbol)
LHS consists of a name 
RHS whatevery 

`LHS ::= RHS`

Each rule is called a production rule - how you expand the symbol of the LHS.
Two types 
- Terminal symbol - cannot be expanded further, (Variable)
- Non terminal symbol is a name you created in sake of defining the rules, found on the left of = (Operation)

### Example: Integers
```
// LHS Non-terminals 
sign ::= +|-
digit ::= 0|1|2|3|4|5|6|7|8|9
number ::= [sign]digit{digit}
```

|  Symbol   |                Meaning                |
| :-------: | :-----------------------------------: |
|    `=`    |            is defnined as             |
|    \|     |                  or                   |
| `(....)`  |               Grouping                |
| `{.....}` | Repetitive items (zero or more times) |
| `[.....]` |     Optional items (none or once)     |
| `"...."`  |   Terminal character/symbol/string    |

Show that -135 is a *legal* number
number 
- Expanded into an optional + or - sign , in this case is minus sign. 
- Followed by a digit - in this case this digit is 1.
- Optional additional digits, two more is 3 and 5
![[Pasted image 20260818102715.png]]

### Syntax Diagram
Sequence Left to Right
![[Pasted image 20260818102953.png]]
-> A -- B -- C -- D
`A B C D`

Choice: Parallel 
![[Pasted image 20260818103002.png]]
`A|B|C|D`

Option: Exist or not, drawn in two branches 
![[Pasted image 20260818103020.png]]
`[A]`

Repetition: Draw an arror back to say it could be repeated, top is one or more times, bottom allows us to skip it. May exist zero or more times
![[Pasted image 20260818103012.png]]
`{A}`

Number described by Ex 1 as a syntax diagram:
(In notebook)

### Example 2:
Recursion
``` racket
expr ::= term | expr (+|-) term
term ::= factor | term (*|/) factor
// can be a factor or a term, mulitplyer or divide another factor
// Term on the right hand side and factor on LHS and RHS so its recursive. 
factor ::= integer | ”(” expr ”)”
integer ::= digit{digit}
digit ::= 0|1|2|3|4|5|6|7|8|9
```
Number 45:
If you look at it as a term, a term could be a factor, which could be an integer

### Example 3:
```
program ::= PROGRAM identifier
BEGIN {assignment ;} END.
assignment ::= identifier ”:=” (number|identifier|string)
identifier ::= alphabet{alphabet|digit}
number ::= [-]digit{digit}
string ::= {alphabet}|”!”|” ”
alphabet ::= [a-zA-Z]
digit ::= [0-9]
```

Does this EBNF grammar correctly describe this language?
```
PROGRAM DEMO1
BEGIN
A:=3;
B:=45;
H:=-100023;
C:=A;
D123:=B34A;
BABOON:=GIRAFFE;
TEXT:="Hello world!";
END.
```

Yes.

|      Symbol      | Meaning                                  |
| :--------------: | ---------------------------------------- |
|   `< . . . >`    | Non-terminal symbols                     |
|       `+`        | E+ matches one or more occurrences of E  |
| `*` (Kleen star) | E* matches zero or more occurrences of E |
|       `ε`        | Empty string                             |
**Other variations**
Sometimes, terminal symbols are in bold while non-terminals
are in normal font
-> or = may be used instead of ::=


**Grammar**
- The grammar of a language is defined by
	1. Finite set of non-terminal symbols N
	2. Finite set of terminal symbols T
	3. A starting symbol S
	4. Finite set of production rules P
- A program (sentence) contains only terminal symbols
- A sentential form is any string that can be derived from S

Types of languages that we try to define
- Type 2 - context- free grammar
	- in the form of (E)BNF
	- suitable for programming languages

What we are concerned with is Derivation, whether program you right is given to be checked for grammar
- Start with start symbol
- Expand 

Example right derivation
```
expr = id | number | - expr | ( expr )
| expr op expr
op = + | - | * | /
```

Derive: `slope * x + intercept`

Go from LHS or RHS of string.
Expand from right
`expr -> expr op expr`
	`x + intercept` = `expr op expr`
	`x + intercept` = `expr op id`
	= `expr + id`
	`slope * x + intercept`= `expr op expr + id`
	= `expr op id + id`
	= `expr * id + id`
	= `id * id + id`

**Parse tree of RHS**
![[Pasted image 20260818105816.png]]

A tree representation of a derivation based on a grammar
- The root node is the Start symbol
- Each leaf node is associated with a terminal
- Each internal node is associated with a non-terminal

Derive from LHS
`slope * x + intercept`
first expansion from left to right
`expr` = `expr op expr`
first expression (expr) is id 
= `id op expr`
= `id * expr`
= `id * expr op expr`
= `id * id op expr`
= `id * id + expr`
= `id * id + id`
**Parse tree of LHS Derive**
![[Pasted image 20260818110118.png]]

Two different parse trees based on order of sequence 
If you can have different parse trees potentially with different results then Grammar is **Ambiguous**
Not the type of grammar you want for any programming language.

To change this to not be ambiguous. Problem is + or - is treated same as multiply or divide. Which is incorrect, multiply or divide should be treated first.
#### Rearrange the grammar rules

Original: 
```
expr = id | number | - expr | ( expr )
| expr op expr
op = + | - | * | /
```
**Rearranged**:
```
expr = term | expr add_op term
term = factor | term mult_op factor
factor = id | number | - factor | ( expr )
add_op = + | -
mult_op = * | /
```

Some languages brackets are treated differently, in order of sequence, the one with higher precedence is put later so when we expand upwards we encounter the ones with higher precedence first before we encounter the ones with lower precedence.

`slope * x + intercept`
Derive **LHS**
 ```
 expr = term
	 = term mult_op factor
	 = factor mult_op factor
	 = id * factor
	 = id * (expr)
	 = id * expr add_op term
	 = id * term add_op term
	 = id * factor add_op term
	 = id * id add_op term
	 = id * id + factor
	 = id * id + id
 ```
Derive **RHS**
```
expr = expr add_op term
	= expr add_op factor
	= expr add_op id
	= expr + id
	= term + id
	= term mult_op factor + id8
	= term mult_op id + id
	= term * id + id
	= factor * id + id
	= id * id + id
```

#### Limitations
- EBNF cannot express **contextual constraints**
	- Ex: In C, `i = 5;` is valid only if `int i` is declared first
- Could be overcome by adding a second level of rules (in a different metalanguage) – **too complex, not commonly used**
- Deal with this problem by a separate process: **type-checking**