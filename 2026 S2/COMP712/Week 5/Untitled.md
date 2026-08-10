Programming languages
Three aspects to making your own language - Syntax, Semantics, Pragmatics
### Syntax
Any language will have syntax - English
	Two parts -
	Lexical Syntax 
		 Always some special set of words to use (keywords) - you should not use these as your variable names.
		 What constitutes legal identifiers that names variables, functions, and constants. 
		 Operators and punctuation marks - semi colons at the end of a statement etc
	Grammatical Syntax - how to put the words together to form a meaningful sentence
		What is a valid statement in that language, like C always end with a semicolon 
		How we compose larger expressions from smaller expressions - how do we describe what the syntax looks like - what is allowed and not
			**Backus-Naur Form** or its extension
		we use language to describe what the language looks like.
		example x = y + 1 
		(x y) variables , (=) assignment operator , (y + 1) expression that we need to compute, altogether is a statement 

Front-End Processing 
	First part is Scanner or Laxer. The first part is to group all these characters together - produces this stream of Tokens (means a unit of something) then goes through the sequence of tokens produced to make sense and see if its allowed in this language - produces a syntax in a tree form which will be redefined for later use.

Concrete Syntax - that we use to write. 
``` Java
public static int abs (int n) {
	if (n < 0)
		return -n;
	else
		return n;
}
```

``` python
def abs (n) :
	if n < 0 :
		return -n
	else:
		return n
```

Abstract Syntax - A syntax tree
![[Pasted image 20260811101743.png]]

### Semantics
The **Semantics** of a programming language - defines its meaning
	**Static** semantics: something we can understand without having to run the program.
	A question to ask: 
		Are the expressions **well-typed**?  
		What is the **scope** of a variable?
	**Dynamic** Semantics: What will happen when the program runs 
		Will the program **terminate**? - Infinite loops it will never terminate.
		What side effects will it produce? 
		What **outputs** will it produce? - Are the results tidy on the screen

x = y + 1 

What are the semantics? Where the values come from?
As a computer what will that mean?
Means:
Assign memory location.
Add 1 to the content at memory address located where variable ==y== is associated with. 
The result of the addition is to be stored at memory address located where variable ==x== is associated with.
These are the questions the interpreter will be concerned about its different from the programmers perspective. 

Static semantics Example: Type Checking
Which of the ofllowing Java code is well-typed

2 * (3 + 4) (Well typed)
2 < (3 + 4) (Well typed)
2 < True (Not allowed) Boolean and integers cannot mix.
``` Java
if (a < b) {
	c = a + b;
} else {
	c = a * b;
}
```




### Pragmatics
The details that go into your complier that help you do your job.