
Input a sequence of tokens to a parser. Output: a parse tree or an abstract syntax tree
- **Purpose:** check that a program is syntactically correct
- **Input:** a sequence of tokens (from the lexer)
- **Output:** a parse tree or abstract syntax tree (AST)

**Top-down stratergy**

- Start from the **Start symbol** (root of the tree) and expand using production rules, working toward the input
- Stop when the right-hand side of a rule matches input using only terminal symbols
- Called an **LL parser** (Left-to-right scan, Leftmost derivation)
- Also called a **predictive parser**

**Bottom-up stratergy**

- Start from the **input string** itself
- Find a substring matching some rule's right-hand side, replace it with the rule's left-hand side (non-terminal)
- Repeat until only the Start symbol remains
- Tree is built from the **leaves upward**
- Called an **LR parser** (Left-to-right scan, Rightmost derivation), a.k.a. **shift-reduce parser**

Left-most Derivation

Before a program can run , it goes through the two stages:
```
source text  --[LEXER]-->  tokens  --[PARSER]-->  parse tree / AST
```

**Lexing** turns this into a flat sequence of tokens: `IF, LPAREN, IDENT "x", LT, INT 0, RPAREN, LBRACE, RETURN, MINUS, IDENT "x", SEMI, RBRACE, ELSE, ...`

**Parsing** then takes that token sequence and builds a tree structure showing how the tokens relate grammatically (the `if`/`return`/`<` tree shown in the slide) — this is what lets the rest of the compiler/interpreter understand the code's structure, not just its raw text.