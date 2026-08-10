## What is a Complier?
A software that transform computer programs written in one language (source) into another language (target) - A language translator
	Usually refer to a high-level language (Java, C++) and then translate to a lower level language that the computer can execute.

Compiler split into Front-End and Back-End
Front performs Lexical Analysis -> parsing (grammar is correct) -> Semantic Analysis.
	Abstract Syntax Tree - Intermediate Representation
Back End, from syntax tree you produce the syn language, simplify the syntax tree (be translated into some other form) -> Optimize -> Code Generation (The machine code) 
	Output: Object Code

Linker: All the object codes will run through the linker to output executable code.


Scanning and Parsing
Scanning : Divides source text into **tokens** (smallest meaningful units) is it a number, an operator?
Parsing : Recognize a context-free language
	Produces a parse tree

Intermediate Code Simplifications
Lots of different kinds of optimizations some very complex , rewrite a sequence of operations more efficiently by,
- (simple) **Constant folding**: 2 + 3 -> 5
- (complex) **Lift** : an invariant computation out of a loop
- (more complex!) **Parallelize** a loop

Code Generation
Translate intermediate form to target code
Includes:
- Register assignment 
- Instruction Selection
- Instruction Scheduling
Multiple instructions you can use to do multiple things, which one do we use?

![[Pasted image 20260811105432.png]]
## Interpreter
More just front end, the back end of an interpreter is the Evaluator. Sometimes the evaluator is the input of the syntax tree, so the evaluator basically follows the trees branches. 

A program that executes another program on some input, producing an output
	Controls the execution.
Allows users to input and execute program statements on the fly.

Dynamic and Just-in-Time compilers.
Deliberately delay compliation until last possible moment. 
Typically work with interpreters - done in racket, first time you run its interpreted at the same time it compiles it. First time is slow, ready for use for second time.
Only compiled when you use it

C is the standard compiler because its been optimized so many times.

Unconventional Compilers
- Text formatters (e.g. LaTeX)
- Silicon compilers - generate microchip layouts from circuits.
- 