
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
| Token Name | Lexemes |
| --------------| ---------- |
| LPAREN | x foo first 1| 