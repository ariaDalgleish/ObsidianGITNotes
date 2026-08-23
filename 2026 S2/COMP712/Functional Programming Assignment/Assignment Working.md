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

![[Pasted image 20260823171138.png]]
Rubric:

| Excellent                                                                                                                                                                   | Competent                                                                                                                                                                             | Basic                                                                                                                                                                                                                             | Poor / N                                                                                                                                                                                                                                                           |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Explanation is precise and insightful.<br>Revised max-list is correct.<br>All edge cases are handled correctly. <br>Code is clean, functionally styled, and well commented. | Clearly explains inefficiency.<br>Correctly rewrites max-list using let.<br>Handles some edge cases correctly. <br>Code is clean, functionally styles, but could be better commented. | Identified inefficiency but reasoning is partial or imprecise.<br>Revised max-list works on simple lists but minor issues with edge cases.<br>Uses let, but only partially reduces inefficiency.<br>Lack of comments in the code. | Explanation of inefficiency is missing or incorrect.<br>Revised max-list either does not run or has major logical errors.<br>Does not use let appropriately.<br>Code shows weak understanding of recursion and functional style. <br>Lack of comments in the code. |
| 15 to >13 pts                                                                                                                                                               | 13 to >9 pts                                                                                                                                                                          | 9 to >5 pts                                                                                                                                                                                                                       | 5 to >0 pts                                                                                                                                                                                                                                                        |

Questions: 
1. Recursion (Max Mark: 15 / 100)
Analyse the following Racket function max-list.
```
(define (max-list ls)
(if (null? Ls)
-inf.0
(if (> (first ls) (max-list (rest ls)))
(first ls)
(max-list (rest ls)))))
```
Note that -inf.0 represents negative infinity in Racket.
Task:
(a) Explain why it is not as efficient as it could be. Put your answer as comments in
the Racket file.
(b) Rewrite the function using let to make it more efficient.



![[Pasted image 20260823171203.png]]

| Excellent                                                                                                                                                                                                         | Incomplete                                                               | Poor / No attempt |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ | ----------------- |
| Full marks for:<br>(i) Fuction defined as specified<br>(ii) Function works correctly;<br>(iii) Handles edge cases;<br>(iv) No mutation of data;<br>(v) At least 5 different test cases<br>(vi) Adequate comments; | One more more of the following:<br>(i) <br>(ii)<br>(iii)<br>(iv)<br>(iv) |                   |
|                                                                                                                                                                                                                   |                                                                          |                   |

2. Sublist (Max Mark: 15 / 100)
Task: Write a Racket function sublist that takes two lists as arguments. It should return #t if
the first list appears as a contiguous sublist somewhere within the second list and #f
otherwise.
Examples:
``` racket
(sublist ’(c d e) ’(a b c d e f g))  #t
(sublist ’(a c e) ’(a b c d e f g))  #f
(sublist ’(e) ’(a b c d e f g))  #t
```
Note: You are are required to use only the functional features of Racket. Functions with
exclamation point in their names such as set! are not allowed.
Include at least 5 test cases to demonstrate that your code is working correctly. These test
cases should demonstrate that your procedure works under a range of different scenarios
other than the ones provided above.

![[Pasted image 20260823171025.png]]

3. Remember the Past (Max: 25 / 100)
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

Tasks:
(a) Write a Racket function called fmonitor that takes a procedure f as argument,
and returns a procedure (we’ll call it mf here) that takes one argument. When mf
is invoked with a symbol ’how-many-calls? as argument, it should return the
number of times this procedure has been called. Its internal counter should be
reset if the symbol ’reset-count is passed to it instead.
Usage example:
```
(fib 8)  21
(set! fib (fmonitor fib))
(fib 8)  21
(fib ’how-many-calls?)  67
(fib ’reset-count)
(fib ’how-many-calls?)  0
```
(b) Write a procedure named memoize. It takes a procedure f of one argument and
returns a new procedure mf of one argument. The first time mf is called with an
argument value, f should be called and its result kept in a “table”. Subsequent
calls to with the same argument should return the stored value instead of
redoing the computation.
Usage example:
```
(set! fib (memoize fib))
(fib 8)  21
Note that your table could simply be a list of lists as follows:
((1 1) (2 1) (3 2) (4 3) (5 5) . . . )
```
where each sublist (a b) represents (a fib(a))
Therefore, you may want to write helper function(s) to extract the value fib(a) if a
already exists in the table.

![[Pasted image 20260823171109.png]]