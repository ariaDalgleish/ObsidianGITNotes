
Book recommendation: 

Lisp 1, 1.5 (1958) --> Scheme --> Racket (2010)
Program gets too much and then simplier version comes out and then variations of that language. Clojure is like javascript in lisp lol

Both 
- promot functional style with imperative features
- Dynamic types - means no need to declare type of var before you use it, variable can be any type, unlike java or C : a is int... Downside is it can be any type, easy to use wrongly.
Racket is complied - first time takes longer as it compiles code - second time runs faster cause it uses complied code to compile.... ??
- Minimalist syntax - downside it has lots of brackets
	- Macros - extensive and very powerful
	- Modules: each function is local to that file - every definition is private unless exposed to make public (provide(all-defined-out))

Using DR RACKET
start with specifing which language to use ```#lang racket``` or ```#lang slideshow```
True or False: ```#t``` or ```#f``` 
Strings: "hello" 
Characters: #\h 

When you enter an atom the interpreter returns that atom (Basic datatypes like strings characters)

No restrictions for lists
![[Pasted image 20260716183432.png]]

Quote vs List:  Quote treats pi as a symbol, list evaluates pi into a number
![[Pasted image 20260716183612.png]]

Identifier = name of a variable or function/procedure. 
	Can be any string of characters: one  2x3  (is a name)
Symbol = a quoted identifier

No difference with brackets: ()[]{} just make sure you match, start and end with same breacket

S-expression is everything inside brackets. (x . y) where x and y are s-expressions
(x. y) is called a **pair** vs list points to next item to next item. 
(a . ((2 . pi) .x)) two pairs, multiple layers of pairs. each layer of bracket with a dot (.) is has two items

A list is an s-expression  (list 1 2 3)  1 points to 2 points to 3 point to nil (null empty list)
cons cell -> pairs of pointers
![[Pasted image 20260716184648.png]]
car points to value, cdr points to whatever else goes behind it.

``` + is a procedure``` 

General Syntax: 
```(e0 e1 ... eN) ```
Function or special form followed by arguments

Useful list functions:
- list? -> Check if the argument is a list
- null  ' () -> The empty list
- null?  ->  Check if a list is empty
- car   first -> Returns first element of a list
	(car (cons 1 "name)) -> returns 1
- cdr  rest -> Returns everything after first element
	(cdr (cons 1 "name")) -> returns "name"
	(cdr (list 1 "name")) -> returns ("name") , a list 

> (reverse '(1 2 3 4 5))
> '(5 4 3 2 1)
> (append ' (1 2) ' (3 4) ' (5 6))
> '(1 2 3 4 5 6)
> (range 0 10 2)
> '(0 2 4 6 8)
> (null? ' (1 2 3 4 5))
> false (#f) 

first element of s-expression will try to call....

Special Form: Defines
(define x 5) -> returns nothing
(define f (+ x 4)) -> x is now 5 so 5 + 4 = 9! 
(define g (+ x f)) -> g = 14  (5 + 9)
Evaluates the expression then bind it to f

**Defining functions** has same form as something else
(define (<name><arguments>) <body>)
	(define (square x)(* x x))
		function name = square
		argument = x
		function body = (* x x)

Define a procedure 

no news is good news (no errors lol)

Order of Evaluation
- Applicative Order
	- Evaluate arguments, then apply
(+ 5 1) (* 5 2) = 6 10
- Normal Order
	- Fully expand, then reduce
(+ (* (+ 5 1)  (+ 5 1) )
	(* ( 5 2) (* 5 2) ) )
In racket anything that isn't = false is default true. 

Conditional: 
(cond [<e1a> <e1b>]
	[<e2a> <e2b>]
	. . . . .
	[else <eNb>] )
If e1a is true, evaluate e1b, etc.
good practice to use else at end of condition: if nothing else it catches. 