Passing style programming 
- every function explicitly hands its results to that next step

(if (null? x) // what to evaluate
' () // what to do with the evaluated result
  (cdr x) ) // continuation


passing the result - if its empty (0) then pass to k if not then pass along (else)
```
(define (sum-list/cps xs k)
	(cond [(empty? xs) (k 0)]
		[else (sum-list/cps (rest xs)
			(lambda (rest-sum)
				(k (+ (first xs) rest-sum))))]))
```

Continuation passing style (CPS) is useful
Helps to implement:
- Early exit
- Backtracking
- Exception-like behaviour (divide an umber by 00 you can handle it in a more elegant way)
- tail-recursive transformations
- Implement interpreters and compilers

To check for zero in the list, keep going through every element in the list until you find or dont find a zero. If written with CPS two possible, success continuation and return true or failure continuation using recursive cdr of the list. 

CPS Mindset: do not return a result directly;
instead, route control to the appropriate next step

Write the if function using CPS

A function never returns a value, instead it takes an extra argument - a continuation (called k) which is a function representing "what to do with the result." 

Types of constructs, numbers and addition. All you can do is add numbers.
represented as:
```
(struct num (n) #:transparent)
(struct add (l r) #:transparent) // left and right
```

CPS-style Evaluator
expression -> left value -> right value -> add -> continuation
For interpreters, this is powerful because you can change the
continuation to:
– Stop early on an error
– Collect debugging information
– Implement exceptions
– Add sequencing and control operators

this let is called loop. Let "name"
```
(define (find-first-zero xs
	(call/cc
		(lambda (exit)
			(let loop ([xs xs])
				(cond
					[(empty? xs) #f)]
					[(zero? (first xs)) (exit #t)]
					[else (loop (rest xs))])))))
```

