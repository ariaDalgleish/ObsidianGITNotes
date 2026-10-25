Section 1.2 The Programming Language Spectrum

Languages can be classified into families. 

**Declarative** languages --> *what* the computer is to do
	Programmers POV, less implementors POV
	Designed with the desire to get away from "irrelevant" implementation details. Yet stay close enough to the details to control the outline of an algorithm. 

**Imperative** languages --> *how* the computer should do it
	Most common for performance reasons

Important subfamilies:

##### ***Functional*** Languages
- Based on the recursive definition of functions
	- Recursive Function is ==a function that repeats or uses its own previous term to calculate subsequent terms and thus forms a sequence of terms==.  Recursion is when a method calls itself over and over again until it reaches a specific point or value - to achieve an iteration/loop.
- Inspired from lambda calculus (1930s Alonzo Church). 
- Languages: **Lisp, ML** and **Haskell**
- Program is considered a function from inputs to outputs, defined in terms of simpler functions through a process of refinement.

While loop vs Recursion:

```` 
def look_for_key(main_box):
  pile = main_box.make_a_pile_to_look_through()
  while pile is not empty:
    box = pile.grab_a_box()
    for item in box:
      if item.is_a_box():
        pile.append(item)
      elif item.is_a_key():
        print "found the key!" 
````
![](https://drek4537l1klr.cloudfront.net/bhargava/Figures/040fig01.jpg)

Call stacks in recursive: (Calculating factorial of a number)
![[Pasted image 20260716170401.png]]
![[Pasted image 20260716170421.png]]

##### ***Dataflow*** languages
- Flow of information (*tokens*) among primitive functional *nodes*.  Nodes are triggered by the arrival of input tokens, and can operate concurrently. 
- **Id and Val** are dataflow languages. Sisal a descendant of Val is more often described as a functional language.
#### *Logic* or *Constraint-based* languages
- Attempt to find values using goal-directed search through a list of logical rules.
- **Prolog** best known logic language - Excel
##### *von Neumann* Language
- Most familiar and widely used.
- **Fortran, Ada, C** - Computation is the modification of variables.
- Functional languages are based on expressions that have values, von Neumann languages are based on statements that influence subsequent computation - *side effect* of changing the value of memory. 
##### *Object Oriented* languages
- Roots trace to Simula 67. closely related to von Neumann but much more structured and distrubuted model of both memory and computation. 
- Interactions among semi-independant *objects* that each have its own internal state and subroutines to manage that state. 
- Smalltalk (purest language), C++, Java 

##### *Scripting* Languages 
- Coordinating or "gluing together" components drawn from some surrounding context. 
- Developed for specific purposes:
	- **csh and bash** are input languages of job control (shell) programs.
	- **PHP and JavaScript** intended for generation of dynamic web content. 
	- **Lua** control computer games.
	- **Perl, Python, Ruby** deliberately for general purpose.
- Most put an emphasis on rapid prototyping with bias toward ease of expression over speed of execution.

Greatest Common Divisor (GCD) 
von Neumann algorithm:
	`To compute the gcd of and b, check to see if a and b are equal. If so, print one of them and stop. Otherwise, replace the larger one by their difference and repeat.`
		**C Language:** 
		``` int gcd(int a, int b) {
			while (a != b) {
				if (a > b) a = a - b;
				else b = b - a;
			}
			return a;
		} 
		```
Functional - emphasis on the mathematical relationship of outputs to inputs:
	```` The gcd of a and b is defined to be (1) a when a and b are equal, (2) the gcd of b and a - b when a > b, and (3) the gcd of a and b - a when b > a. To compute the gcd of a given pair of numbers, expand and simplify this definition until it terminates. ````
		The key work *let* introduces a definintion; rec indicates that it is permitted to be recursive; arguments for a function come between the name (gcd) and the equals sign
	**OCaml**
	```` let rec gcd a b =
		if a = b then a
		else if a > b then gcd b (a - b)
			else gcd a (b - a)
	````
Logic - programmer specificies a set of axioms and proof rules that allows the system to find desired values:
	The proposition gcd (a, b, g) is true if (1) a, b, and g are all equal; (2) a is greater than b and there exists a number c such that c is a - b and gcd (c, b, g) is true; or (3) a is less than b and there exists a number c such that c is b - a and gcd(c, a, g) is true. To compute the gcd of a given pair of numbers, search for a number g (and various numbers c) for which these rules allow one to prove that gcd (a, b, g) is true.
	**Prolog**
	````gcd (A,B,G) :- A = B, G = A.
	gcd(A,B,G) :- A > B, C is A-B, gcd(C,B,G).
	gcd(A,B,G) :- B > A, C is B-A, gcd(C,A,G).
	```` %%Read :- as "if" and "and" for commas %%

General flavors of the families without formal definitions ^^ they blur together some languages.