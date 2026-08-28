# Submission Requirements:

1. Submit your answers to the following questions before the due date via Canvas.
Refer to the marking rubric for the marking scheme.
2.  The procedures for each question should be contained in its own Racket file, one
file per question. Name each file Qx.rkt where x is the question number. For
questions with multiple parts, put the code for each part in the same Racket file
and do not split them into separate files.
3.  Your Racket programs should be documented with suitable comments. Your
name should be the first comment after #lang racket.
4.  You may not use additional Racket libraries unless otherwise allowed by the
question. In other word, you should not have the line `(require <library-name>)` in
your files.



### (Q1) Recursion (Max Mark: 15 / 100)

| Question 1 Rubric | Excellent                                                                                                                                                                   | Competent                                                                                                                                                                             | Basic                                                                                                                                                                                                                             | Poor / N                                                                                                                                                                                                                                                           |
| ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
|                   | Explanation is precise and insightful.<br>Revised max-list is correct.<br>All edge cases are handled correctly. <br>Code is clean, functionally styled, and well commented. | Clearly explains inefficiency.<br>Correctly rewrites max-list using let.<br>Handles some edge cases correctly. <br>Code is clean, functionally styles, but could be better commented. | Identified inefficiency but reasoning is partial or imprecise.<br>Revised max-list works on simple lists but minor issues with edge cases.<br>Uses let, but only partially reduces inefficiency.<br>Lack of comments in the code. | Explanation of inefficiency is missing or incorrect.<br>Revised max-list either does not run or has major logical errors.<br>Does not use let appropriately.<br>Code shows weak understanding of recursion and functional style. <br>Lack of comments in the code. |
| /15 pts           | 15 to >13 pts                                                                                                                                                               | 13 to >9 pts                                                                                                                                                                          | 9 to >5 pts                                                                                                                                                                                                                       | 5 to >0 pts                                                                                                                                                                                                                                                        |
Analyse the following Racket function `max-list`.
```
(define (max-list ls)
(if (null? Ls)
-inf.0
(if (> (first ls) (max-list (rest ls)))
(first ls)
(max-list (rest ls)))))
```
Note that `-inf.0` represents negative infinity in Racket.

**Task**:
1. Explain why it is not as efficient as it could be. Put your answer as comments in the Racket file.
2. Rewrite the function using `let` to make it more efficient.

### (Q2) Sublist (Max Mark: 15 / 100)

| Question 2 Rubric | Excellent                                                                                                                                                                                                         | Incomplete                                                                                                                                                                                                                      | Poor / No attempt                    |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------ |
|                   | Full marks for:<br>(i) Fuction defined as specified<br>(ii) Function works correctly;<br>(iii) Handles edge cases;<br>(iv) No mutation of data;<br>(v) At least 5 different test cases<br>(vi) Adequate comments; | One more more of the following:<br>(i) Function not defined as specified;<br>(ii) Function does not work in some cases;<br>(iii) No or insufficient test cases provided;<br>(iv) Mutation is used;<br>(iv) Inadequate Comments. | Function not defined or does not run |
| /15 pts           | 15 to >13 pts                                                                                                                                                                                                     | 13 to >1 pts                                                                                                                                                                                                                    | 1 to >0 pts                          |

**Task**: Write a Racket function sublist that takes two lists as arguments. It should return #t if
the first list appears as a contiguous sublist somewhere within the second list and #f
otherwise.
Examples:
``` racket
(sublist ’(c d e) ’(a b c d e f g))  #t
(sublist ’(a c e) ’(a b c d e f g))  #f
(sublist ’(e) ’(a b c d e f g))  #t
```
**Note**: You are are required to use only the functional features of Racket. Functions with
exclamation point in their names such as `set!` are not allowed.

Include at least 5 test cases to demonstrate that your code is working correctly. These test
cases should demonstrate that your procedure works under a range of different scenarios
other than the ones provided above.

### (Q3) Remember the Past (Max: 25 / 100)

| Question 3 Rubric | Excellent                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | Incomplete                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Basic                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | Poor / No attempt                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|                   | fmonitor is robust, idiomatic, and demonstrates a clear understanding of lexical scope and closures for maintaining internal state. <br>memoize is well-designed, with clean helper functions and a clear functional abstraction for caching; handles a wide range of argument values correctly. Implementation shows thoughtful handling of edge cases while respecting the one-argument constraint. Code is well organized, thoroughly commented. Usage examples and any additional tests convincingly illustrate correct and efficient behaviour. | fmonitor correctly wraps a one-argument procedure, count calls, and responds properly to 'how-many-calls? and 'reset-count. <br>memoize correctly stores and retrieves prior results and avoids recomputation for repeated arguments. Helper functions for table lookup and update are clearly defined and functionally implemented. Code reproduces the given usage examples for fib correctly and demonstrates good understanding of higher-order functions and closures. Design and documentation are clear, with sensible structure. | fmonitor roughly follows the specification but has issues (e.g. miscounts calls, incorrect handling of 'how-many-calls? or 'reset-count).<br>memoize caches some values but fail on certain arguments or not retrieve stored results correctly. Uses lists or similar structures to store data, but lookup or update logic is fragile or inefficient.<br>Functional style is mixed with ad-hoc state management; code works for simple examples but lack robustness.<br>Usage examples mostly work, but behavior is not fully aligned with the specification. | fmonitor and/or memoize are missing or substantially incorrect.<br>Returned procedures do not match the required interface (e.g. wrong arity, symbols not handles as specified).<br>Call counting and reset logic do not work correctly or rely heavily on mutation in ways that break the intended behavior.<br>Memoization table is absent or incorrectly implementedl repeated calls recompute insted of reusing results. <br>Usage examples for fib cannot be reproduced correctly. |
| /25 pts           | 25 to >23 pts                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | 23 to >14 pts                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | 14 to >5 pts                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | 1 to >0 pts                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |

In the lecture, we have written a procedure to compute the Fibonacci sequence as
follows:
```
(define (fib n)
(if (< n 2)
n
(+ (fib (- n 1) (fib (- n 2)))))
```
One of the disadvantages of this procedure is that it computes the same values over
and over again. We will monitor this situation by (a) writing a procedure that helps to
track the number of times a procedure is called, and (b) keep a list of prior results in
a table so that if called upon to compute something that’s already been computed,
then the prior result will be returned without repeating the computation.

**Tasks:**
1. Write a Racket function called **fmonitor** that takes a procedure *`f`* as argument, and returns a procedure (we’ll call it *`mf`* here) that takes one argument. When *`mf`* is invoked with a symbol **`’how-many-calls?`** as argument, it should return the number of times this procedure has been called. Its internal counter should be reset if the symbol **`’reset-count`** is passed to it instead.

Usage example:
```
(fib 8)  21
(set! fib (fmonitor fib))
(fib 8)  21
(fib ’how-many-calls?)  67
(fib ’reset-count)
(fib ’how-many-calls?)  0
```

2. Write a procedure named **`memoize`**. It takes a procedure *`f`* of one argument and returns a new procedure *`mf`* of one argument. The first time *`mf`* is called with an argument value, *`f`* should be called and its result kept in a “table”. Subsequent calls to with the same argument should return the stored value instead of redoing the computation.

Usage example:
```
(set! fib (memoize fib))
(fib 8)  21
Note that your table could simply be a list of lists as follows:
((1 1) (2 1) (3 2) (4 3) (5 5) . . . )
```
where each sublist `(a b)` represents `(a fib(a))`
Therefore, you may want to write helper function(s) to extract the value `fib(a)` if `a`
already exists in the table.

### (Q4) Functional Event Stream Processor (Max Mark: 45 / 100)

| Question 4 Rubric | Excellent                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Incomplete                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | Basic                                                                                                                                                                                                                                                                                                                                     | Poor / No attempt                                                                                                                                                                                                                                                                                                                                                                      |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|                   | Event stream processor is fully correct, robust, and exemplifies functional programming principles throughout.<br>Stream transformers and pipelines form a coherent, extensible library;<br>abstractions are well-chosen and could be reused in other contexts. <br>Appropriate use of higher-order functions is evident.<br>Analytics applications are well designed and structured; code runs correctly.<br>Test cases fo both moving average and drop-off detection are comprehensive, systematically cover normal and edge scenarios, and are well documented. <br>Overall design and implementation show excellent mastery of Racket functional programming and go beyond the minimum specification in a meaningful way. | Event struct and immutable list streams are correctly defined and use consistently. <br>All required transformers (map-stream, filter-stream, window-stream, aggregate-stream) are implemented as pure, higher-order functions. Pipelines are first-class values and can be composed functionally. <br>Pre-sensor moving average and drop-off detection work correctly for typical inputs, with reasonable handling of window size sensor selection,, and thresholds. At least 5 meaningful test cases for each analytic task, including one or more edge cases, are provided and demonstrate correctness. <br>Code is clear with appropriate documentation. | Applications run inconsistently.<br>Some attempts at pure functions, but design mixes stateful and stateless code.<br>Limited use of higher-order functions.<br>Only partial implementation of the pipeline, e.g. basic filtering/mapping, windowing or aggregation is missing or flawed.<br>Test cases are limited in number or variety. | Applications do not  run or is substantially incomplete. Use of mutation.<br>Minimal or no use of higher-order functions; stream processing done via ad hoc recursion or repetition.<br>Event stream representation unclear, inconsistent, or not clearly immutable. <br>Required functionalities (stream transforms, windowing, aggregation, analytics) largely missing or incorrect. |
| /45 pts           | 45 to >36 pts                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | 36 to >25 pts                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | 25 to >9 pts                                                                                                                                                                                                                                                                                                                              | 9 to >0 pts                                                                                                                                                                                                                                                                                                                                                                            |
**Important**: Do not use the Racket stream functions provided in racket/stream as described on this page: https://docs.racket-lang.org/reference/streams.html

**Task**: Design and implement a purely functional event stream processing system in Racket.
You are given a sequence of time-stamped events of the form:
```
(timestamp, sensor, value)
```
where `timestamp` is a non-negative integer, `sensor` is a symbol representing that sensor, and `value` is any number.

Your task is to build a composable pipeline system using higher-order functions that
processes these streams. **Note that for this question, “stream” is just a list, not a real stream.**

#### Requirements:
1. Represent event as a Racket struct.
2. Represent event streams as an immutable list.
3. Implement a library of higher-order stream transformers:
4. All transformations must be pure functions, i.e. no mutation, no global state.
	1. **map-stream** : applies a transformation to each event
		` (event -> event)`
		` (listof event) -> (listof event)`
	2. **filter-stream** : filters events based on predicates
		`(event -> boolean)`
		`(listof event) -> (listof event)`
	3. **window-stream** : groups events into sliding or tumbling windows based on time
		`(listof event) window-size -> (listof (listof event))`
	4. **aggregate-stream** : reduces each window using a user-defined aggregation function
		`((listof event) -> any)`
		`(listof (listof event)) -> (listof any)`
5. (v) Allow piplines to be composed functionally, e.g.
	```
	(define pipeline
	(compose
	(aggregate-stream . . .)
	(window-stream . . .)
	(map-stream . . .)
	(filter-stream . . .)))
	```
#### Contraints:
1. No mutation, i.e. use of set!, mutable structs, etc.
2. Use higher-order functions extensively
3. Pipelines must be first-class values (functions returning functions or composed functions)
#### Application:
Use your implementation to perform the following non-trivial analytics tasks:
1.  Per-sensor moving average with different window sizes
	Usage example:
	`(define mavg-s2-10 (sensor-mavg-pipeline ’s2 10 sample-events))`
		should return the moving average of sensor **`s2`** with a window size of **`10`** from a list of events called **`sample-events`**.
2. Detect events whose value falls sharply from previous window
	Usage example:
	`(define dropoffs (dropoff-windows sample-events 10 15.0))`
	should return the events with value that is **`15.0`** or more below the average value of the previous window of size **`10`**.

Provide 5 test cases, including one or more edge cases, for each application.
Note that you may need to define additional functions


---

# Course Topics Summary 

1. Week 1
	1. Paradigms
	2. Racket Basics (Functional Programming)
		1. Intro to DrRacket, strings, lists, numbers
		2. (self study) Section 1.2 The Programming Language **Spectrum**
			1. Recursion vs Loop
2. Week 2
	1. Immutable and Mutable Data
	2. Pure Functions and Side Effects
	3. Higher-order functions
		1. Lambda function, let, cons, helper function, letrec, map, apply, foldl, foldr, acc
3. Week 3
	1. Recursion 
		1. Map and Tree
		2. Procedure to return a list (flattened and depth)
	2. Data Abstraction
		1. Rational numbers, defined types, operator and predicate procedures
		2. Data Structure Representation
			1. Structs
4. Week 4
	1. Streams
		1. Evaluation
		2. For
	2. Further Examples with fold
	3. Continuation
		1. (CPS)
5. Week 5
	1. Compilers and Interpreters
	2. Elements of Programming Languages
		1. Syntax, Semantics, Pragmatics
	3. Lexical Analysis Regular Expressions
		1. Tokens
		2. Regular Expressions
6. Week 6
	1. Syntax and Grammar
		1. EBNF Control forms
		2. LHS & RHS