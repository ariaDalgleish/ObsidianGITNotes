Recap:
LET Language 

Extend a language in certain ways, PROC implements procedures.
Extend LET to include user-defined procedures/functions.

Syntax:
program = expression
expression = number

![[Pasted image 20260929100528.png]]

Example Program:
``` racket
let x = 200
in let f = proc (z) –(z,x)
	in let x = 100
		in let g = proc (z) –(z,x)
			in –((f 1), (g 1))
```
define function g, last expression is the expression we want to evaluate, evoke the function f with the argument 1, 


Update the grammar:
Code using the rules. 

| Naming of the rules:                                                                                                                                                                 |                                                                                            |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ |
| • Constant expression<br>• Zero? Expression<br>• If expression<br>• Difference expression<br>• Variable expression<br>• Let expression<br>• Proc expression<br>• Call expression<br> | const-exp<br>zero?-exp<br>if-exp<br>diff-exp<br>let-exp<br>var-exp<br>proc-exp<br>call-exp |

What do we want in the procedure?
The body of the function and the argument.

Proc datatype:
```
(define-datatype proc proc?
(procedure
(var symbol?) <------------ Variable (argument)
(body expression?) <------- Body
(env environment?))) <----- Environment
```

An extractor unpacks the value from the expressed-value variant and signals an error if the variant is wrong.