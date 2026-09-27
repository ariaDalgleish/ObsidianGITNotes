
Token is the smallest meaningful chunk of text a programs source gets broken into. The output of the **lexer** (a.k.a scanner) before parsing even starts.

SLLGEN is the tool that generates the datatypes and a parser automatically.

TO write an interpreter you need to turn a string of source code into a data structure - abstract tree - that the interpreter can walk over with `cases.` 
With SLLGEN you write a grammar once and it generates both the `define-datatypes` for the AST and a parser that builds instances of them.


## Calculator Grammar
```
program = expr
expr = term | expr add_op term
term = factor | term mult_op factor
factor = number | "(" expr ")"
add_op = "+" | "-"
mult_op = "*" | "/"
```
Standard arithmetic calculator.
Expressions made of terms added/subtracted, terms made of factors multiplied/divided, factors are numbers or parenthesized expressions. The problem is `expr = expr add_op term` is left-recursive, the rule for `expr` refers to itself as its own symbol. it would recurse into `expr` forever.


## LL(1) Grammar

```
program = expr
expr = term { add_op term }
term = factor { mult_op term }
factor = number | "(" expr ")"
```
**The fix**
The curly brackets means "zero or more repetitions." This rewrites the left-recursive rule into an equivalent **iterative** (right-recursive in practice) form that a predictive top-down parser can handle. Standard trick of eliminating left recursion so a grammar is **LL(1)** (parseable left-to-right, leftmost-derivation, with 1 token of lookahead).

## Lexical Grammar
``` racket
(define lex-num
 '((whitespace (whitespace) skip)
   (comment ("%" (arbno (not #\newline))) skip)
   (number (digit (arbno digit)) number)
   (number ((arbno digit) "." digit (arbno digit)) number)
   (number ("-" digit (arbno digit)) number)
   (number ("-" (arbno digit) "." digit (arbno digit)) number)))
```
**Turning characters into tokens**
This is the **lexer** spec. It says how to chop raw text into tokens.
- whitespace and `%` comments are recognized and thrown away (`skip`)
- numbers can be: plain integers, decimals, negative integers, negative decimals
- `arbno` means "arbitrary number of" (`*` in regex terms - zero or more)
## Grammar
```
(define cal-grammar
 '((program (expression) a-program)
   (expression (term expression+) an-exp)
   (expression+ ("+" term expression+) an-add-exp)
   (expression+ ("-" term expression+) a-sub-exp)
   (expression+ () null-exp)
   (term (factor term+) a-factor)
   (term+ ("*" factor term+) a-mult-term)
   (term+ ("/" factor term+) a-div-term)
   (term+ () null-term)
   (factor (number) a-number)
   (factor ("(" expression ")") a-group)))
```
**-> AST datatypes**
Mirrors the **LL(1) grammar** just with a variant name tacked onto each production. Each rule becomes a variant of a `define-datatype`
- `program` -> one variant `a-program`
- `expression` -> one variant `an-exp` a term followed by an `expression+`
- `expression+` -> three variants: `an-add-exp`, `a-sub-exp`, or `null-exp`
- `term`/`term+` multiplication or division
- `factor` -> `a-number` or `a-group`


| Stage                      | Form                                                            | Problem it solves                                                                                                                       |
| -------------------------- | --------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| Grammar 1                  | `expr = term \| expr add_op term`                               | Natural by left-recursive.<br>Unusable by a top-down parser                                                                             |
| Grammar 2<br>(LL(1))       | `expr = term { add_op term }`                                   | Left recursion eliminated<br>`A = Aα\|β → A = β{α}`                                                                                     |
| Grammar 3<br>(cal-grammar) | `expression+` with `an-add-exp`/`a-sub-exp`/`null-exp` variants | `{ }` repetition re-expressed as right-recursive **datatype** with a base case. <br>SLLGEN can generate `define-datatype`s and a parser |

Exercise:
```
statement ::= "begin" (statement ";")* "end"
		::= "while" expression "do" statement
		::= identifier ":=" expression
expression ::= identifier 
		::= "("expression "+" expression ")"
```
Examples:
```
begin x := foo;
while x do x := (x + bar) end
```