High-order Functions

let vs let* 
are body of the function creates an environment that contains the body of the function and local variables...
let is done simultaneous 
let* is sequential (one-by-one)

lambda is used to create anonymous functions (functions without a name)
λ = lambda
syntax: (lambda (args) body-expression)

// open bracket
``` 
(lambda (a b)
	....
		....)
```

using **helper** function
```
(define (square x)
  (* x x))

(define (f1 x y)
  (define (f-helper a b)
    (+ (* x (square a))
       (* y b)
       (* a b)))
  (f-helper (+ 1 (* x y))
            (- 1 y)))
```

Use **lambda** instead of *f-helper*
```
(define (f2 x y)
  ((lambda (a b)
     (+ (* x (square a))
        (* y b)
        (* a b)))
   (+ 1 (* x y))
   (- 1 y)))
```

Replace using ```let``` 
```
(define (f3 x y)
	(let ([a (+ 1 (* x y))]
		  [b (- 1 y)])
		(+ (* x (square a))
		   (* y b)
		   (* a b))))
```

``` Letrec ```
Expressions are evaluated *in order* in the environment that includes *all* bindings.

```
#lang racket

(define (test-even-odd num)
	(letrec ([even? (λ (x)
			(if (= x 0)
				#t
				(odd? (- x 1))))]
		[odd? (λ (y)
                        (if (= y 0)
                            #f
                            (even? (- y 1))))])
		(list (even? num) (odd? num))))

> (test-even-odd 4)
'(#t #f)
> (test-even-odd 5)
'(#f #t)
> 
```

**Map** is a function that takes a function and a list as arguments
Applies the function to each item in the list -> returns a new list.
```
(map (lambda (x) (+ 5 x))
	(list 1 2 3))

> '(6 7 8)
```

**Apply** a procedure to the element in a list
```
(apply string-append ' ("Hello" " " "World!"))
> Hello World!
```

**Fold**
foldl (LEFT) or foldr (RIGHT)
also known as *reduce*

foldl starts with first item in the list 
(foldl - 0 ' (1 2 3 4)) 
start with 0 and apply - and then go through the list 
> (- 4 (- 3 (- 2 (- 1 0)))) start with 0 and then apply to first item, then 2nd item
> result = 2

foldr starts from the end of list going reverse order
(foldr - 0 ' (1 2 3 4))
(-1 (- 2(- 3(- 4 0))))
>result = -2

(foldl add (* 2 3) (list 1 2 3))
= 12! 2 * 3 = 6 + 1 + 2 + 3 = 12

Implement filter using foldr - behaves the same way as foldr 

filter: Walks through a list and keeps only items that pass the test I gave.

```
(filter (lambda (x) (> x 5)) (list 5 6 7))
```
Check 5: is 5 > 5 ? No -> #f -> dropped
Check 6: is 6 > 5 ? Yes -> #t -> kept
Check 7: is 7 > 5 ? Yes -> #t -> kept
Result = '(6 7)

```
(define (foldr-filter pred lst
(foldr fn // function needs to check if false 
       init // initial item will be empty list '()
       lst)))
```

```
;; Implement filter by foldr
(define (foldr-filter pred lst)
(foldr (lambda (x acc)
       (if (pred x)
           (cons x acc)
           acc))
       '()
       lst))
```

cons is short for construct
```
(cons 1 '(2 3))
;; => '(1 2 3)
```
builds a pair — it sticks one item onto the front of something else (usually a list). Short for "construct." 
It takes two arguments:
1. The thing you want to add
2. The thing you're adding it to (often a list, but could be another single value)

```
(cons 5 '())        ;; => '(5)         -- adding 5 to an empty list
(cons 1 (cons 2 '()))  ;; => '(1 2)    -- building a list piece by piece
(cons 'a '(b c))     ;; => '(a b c)
```

acc stands for accumulator 
imagine you're walking through items one by one, carrying a basket (`acc`). Every time you find an item that passes the test, you drop it in the basket. By the time you've walked through the whole list, the basket contains your final answer — that's your accumulator.

```
(lambda (x acc)
  (if (pred x)
      (cons x acc)
      acc))
```
- `acc` starts out as `'()` (the initial seed you gave `foldr`)
- Each time the lambda runs, `acc` holds "the filtered list built from everything processed so far"
- If `x` passes the test, you `cons` it onto `acc`, growing it by one
- If `x` fails, you just pass `acc` through unchanged — nothing added