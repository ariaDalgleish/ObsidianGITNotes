Defining streams.

Define power of two.
``` Racket
(define powers-of-two
	(letrec ([f ((lamba (x)
		(cons x (lamba ()
			(f (* x 2))))))])
	(lamba (f))))
```

Write a procedure called numbers-until that takes a stream and a function as arguments.

Iterate through numbers produced by the stream until the predicate function returns true.

car - the head
cdr - the rest
cons - joins a pair.
thunk - function with no arguments that is used to delay the evaluation of an expression.

Delayed Evaluation
``` Racket
(define a (+ 25))

/* Evaluated immediately when a is defined. 
Use Thunk to delay this */ 

(define a (lamba () (+25)))
		// thunk
```
A zero argument function defined for purpose of delaying evaluation.
Now only evaluated when a is called.

lamba is used to create functions without a name.

Streams are lazy lists. Each cell of a stream is suspended and is forced only when required.

for - iterations
``` Racket
(for ([i (in-range 273)])
	(writeIn i))
```
be careful of never ending loops. #:break (7 i 10)
difference with for an for* 
`*` - Increments at same time.
for* i)
	j)