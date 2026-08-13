
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
Keyword "FLOAT" IF(find0) LPAREN (left parenthesis) CHAR STAR ID(s) RPAREN LBRACE IF LPAREN BANG ID(strncmp) LPAReN ID(s) COMMA STRING(0.0) COMMA NUM(3) RPAREN RPAREN RETURN REAL(0.0) SEMI RBRACE EOF