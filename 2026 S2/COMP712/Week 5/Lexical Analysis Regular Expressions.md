https://regex101.com/

Types of tokens

simple like operators, minus, divide
logic operators , "and" , 'or"

bound to be a set of keywords

punctuators - "commas", "brackets"

literals - "numbers" "strings" "true or false"

identifiers - user defines variable names, function names

every language will have a set of meaningful tokens, it is up to us to identify what is a valuable token.

Lexer takes a sequence of characters and trying to specificy what the tokens should be. Once founda match you contrust the token............

Lexeme - a sequence of chars that matches the pattern for a token.
Tokens - a token name and an optional attribute (identifier or ....)

| Token Name      | Lexemes        |
| --------------- | -------------- |
| ID (Identifier) | x foo first 1  |
| LPAREN          | (              |
| NUM             | 24 0 921       |
| REAL            | 1.325 0.3 1e22 |
| COMMA           | ,              |
| IF              | if             |
| COMPARISON      | < == >=        |

| Non Token              | Examples |
| ---------------------- | -------- |
| Comments               | /* */*   |
| Preprocessor directive | #nclude  |
| blanks                 |          |
| macros                 | #define  |
| tabs                   |          |
| new lines              |          |
|                        |          |
```
float find0(char *s) /* find a zero */
{ if (!strncmp(s, ”0.0”, 3))
return 0.;
}
```
Sequence of Tokens:
Keyword "FLOAT" , IF(find0) , LPAREN (left parenthesis) , CHAR , STAR,  ID(s), RPAREN, LBRACE, IF, LPAREN, BANG, ID(strncmp), LPAReN, ID(s), COMMA, STRING(0.0), COMMA, NUM(3), RPAREN, RPAREN, RETURN, REAL(0.0), SEMI, RBRACE, EOF

C has more than 100 kinds of tokens:
44 keywords (if, return, double)
integer ,floating ,point ,character ,string 
54 punctuators (+, * , = , -)


### Scanners / Lexers
**Group a sequence of characters into lexical tokens**
Metalanguage – Specify lexical tokens using regular expressions
Implement lexers using deterministic finite automata (DFA)
Lexer generators produces a lexer program in a certain programming
language
– Flex, re2c, RE/flex (C/C++)
– JavaCC (Java)
– SLLgen (Racket) - A lexer and parser generator we will be using

### Regular Expressions (regex)
`\ `(escape character) will match. To use (`.`) you put `\.` to match the dot and `\?` matches a question
- (`.`) is a Wildcard
	- matches any character except newline
	- caution as it matches with any character
- Character set (`[...]` )
	- to match a set of characters
	- Ranges: `[a - z]` (lowercase) `[A - Z]` uppercase `[0 - 9]` 
	- Combine: `[A-Fa-F]`
	- Matches any character enclosed, e.g `[abc]` matches one of a, b, c
- Alternative (`|`)
	- Or, e.g `cat | dog` matches "cat" or "dog"
- Grouping - use brackets to group `(ab)|(cd)` instead of `ab|cd`
- Repetition
	- `e*` matches e zero or more times (`*` is known as Kleen Star)
	- `e+` matches e one or more times
	- `e?` matches e zero or one time
- Anchors
	- `^` match from beginning or `$` end of string, pattern, line.
	

Regular expression that matches any unsigned integer:
`[0-9]` one character out of that range with `+` 
`[0-9]+` can be `7864` `0` `532` `35` can't be `f` 

Regular expression that matches any signed integer:
An integer with a sign in front of it `+` or `-` 
either plus or minus is alternatives, we only want it happening once
`(+|-)?[0-9]+` 
`?` Happening once  `(+|-)` this or that 

Regular expression that matches any real number:
`(+|-)?[0-9]+([\.][0-9]*)`
