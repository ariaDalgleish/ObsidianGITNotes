Lists
Procedure list-length. The argument is a list and I want to return an integer.

Recursive Solution:
Establish the base case : An empty list.

(list-length ' ()) => 0

Implementation
```
(define (list-length ls)
	(if (null? ls) ------ Condition
		0  -------------- True, then return this
		( . . .))) -------- False, then return this
	
			(list-length (rest ls)) ----- Returns the
							length of the rest of the list
							(one less than length of ls)
							
		(+ 1 (list-length (rest ls))) --- Corrent length
											of ls
```

How it works:

```
(list-length ' (a (b c) d) )
=>	(+ 1 (list-length ' ( (b c) d) ) )
=>	(+ 1 (+ 1 (list-length ' (d) ) ) )
=>	(+1 (+ 1(+ 1 (list-length ' ( ) ) ) ) )
=>	(+1 (+1 (+ 1 0) ) )
=>	(+1  (+1 1) )
=>	(+1 2)
=>	3
```

Recursion is preferred in functional programming because it avoids mutation of values, it is not efficient.


| Predicate |   Works on   | Meaning                                               |
| :-------: | :----------: | ----------------------------------------------------- |
|    eq?    |  Any Value   | Object identity<br>Point-like comparison              |
|   eqv?    |  Any Value   | Like eq? but more reliable for numbers and characters |
|  equal?   |  Any value   | Deep structural equality                              |
|     =     | Numbers only | Numeric equality                                      |
 
![[Pasted image 20260728110924.png]]

### Tail Recursive
Is when a recursive call is the last thing executed by a function. Allowing the call stack to reuse stack frames rather than building up the call stack, avoiding stack overflow issues.

Fibonacci Numbers in Racket are integer sequences where each value is the sum of the two preceding ones.

Remove-all " ". Remove all occurrences of an item from a list:
(remove-all 'a' ( (a b (c a) ) (b (a c) a) ) )
=> ( (b (c) ) (b (c) ) )

first check for head of the list - remove first item so now remove the rest of the items in the list. Dealt with head, deal with the rest. 
what if head item is not.... check if item of original list is a ls? if it is a ls then remove all of rest of the list - two lists. Results? two answers, put them back together. 

```
(define (remove-all item ls)
  (cond [(null? ls) '()]
        [(equal? (first ls) item) (remove-all item (rest ls))]
        [(pair? (car ls)) (cons (remove-all item (first ls))
                                (remove-all item (rest ls)))]
        [else (cons (first ls) (remove-all item (rest ls)))]))
```

pair? is a predicate function that checks if a value is a pair (a container that joins two values together using cons) 

cons - creates a new cell that contains the new value and then points to the existing list. 

cons builds a pair. it takes two values and puts them together.
```
(cons  1 2) ; => '(1 . 2)
```

A  list is just nested pairs (list 1 2 3) is shorthand for:
```
(cons 1 (cons 2 (cons 3 '( ) ) ) )
```
each cons cell has two slots, traditionally called car (first element) and cdr (rest)
```
(car (cons 1 2) ) ; => 1
(cdr (cons 1 2) ) ; => 2
```

Pair? checks "is this thing a cons cell"
```
(pair? (cons 1 2))     ; => #t
(pair? '(1 2 3))       ; => #t  (a non-empty list is made of pairs)
(pair? '())            ; => #f  (empty list is NOT a pair — it's its own special value)
(pair? 5)               ; => #f  (an atom, not a pair)
(pair? "hello")         ; => #f
```



Write a procedure depth that returns the number of levels of a list...
```
(define (list-depth ls)
  (if (not (pair? ls))
      0
      (max (add1 (list-depth (first ls)))
           (list-depth (rest ls)))))
```

Base case: if ls isn't a pair at all, depth is 0
Recursive case: if ls is a non-empty list, compare two things and take the bigger:
- (add1 (list-depth (first ls) ) )
	- go one level deeper into the *first* element and add 1 for having descended into it
- (first-depth (rest ls) ) 
	- check the depth of the *rest* of the list, at the *same* level (no add1, since we haven't gone deeper, just sideways)

This walks the list head-by-head: peel off *first*, recurse into it (going deeper), then recurse on *rest* (staying at the same level), and let *max* figure out which path was deepest.

``(list-depth '(1 (2 3) 4 ) )`` :
- Compare ``1 + depth(1)`` = ``1 + 0`` = ``1`` , vs `depth( ( 2 3) 4)`
- That second call eventually finds `(2 3)` sitting in one level in, contributing depth 2 overall
- Final max is 2.