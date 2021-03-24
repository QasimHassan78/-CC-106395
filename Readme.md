#CC Spring 2021: Project Phase 1#
###PROJECT MEMBERS###
StdID | Name
------------ | -------------
**62357** | **Qasim Hassan** <!--this is the group leader in bold-->
62352 | Hamza Tanveer
<!-- Replace name and student ids with acutally group member names and ids-->

## Language Selected ##
Mini c
<!--Replace with your choice-->
## Example of main constructs ##
```
int main ()
{
  float cos, x, n, term, eps, alt;
  // compute the cosine of x to within tolerance eps
  // use an alternating series

  x = 3.14159;
  eps = 0.1;
  n = 1;
  cos = 1;
  term = 1;
  alt = -1;
  
  while (term>eps)
  {
    term = term * x * x / n / (n+1);
    cos = cos + alt * term;
    alt = -alt;
    n = n + 2;
  }
}
```

## Lexical Specification##
the lexical elements of Mini-C. Whitespace is ignored, anything following \\ to the end of
the line is treated as a comment, and keywords and identifiers are case sensitive. If you use the -d option, YACC will generate a header file y.tab.h containing the appropriate constants for multi-character tokens:
yacc -d minic.y
This header file will also define YYSTYPE which is used to define semantic stack attributes for the various terminals and non-terminals in the language

    Local and global variables, parameters.
    Functions, if, while, do``while, return.
    =, ?: (ternary), ||, &&, ==, !=, <, >=, +, -, *, ++, -- (post-ops), !, - (unary), [], ()
    Integer, character, true and false literals. String literals, with automatic concatenation.
    The language it implements is typeless. Everything is a 4 byte signed integer.
    Pointer indexing works in increments of 4 bytes, pointer arithmetic is byte-by-byte.

## Language CFG ##
program -> decl_list

decl_list -> decl decl_list'
decl_list' -> decl decl_list' | ϵ
decl -> var_decl | fun_decl

var_decl -> type_spec IDENT var_decl'
var_decl' -> ; | [ ] ;

type_spec -> VOID
            | BOOL
            | INT
            | FLOAT

fun_decl -> type_spec IDENT ( params ) compound_stmt

params -> param_list | VOID
param_list -> param param_list'
param_list' -> , param param_list' | ϵ
param -> type_spec IDENT param'
param' -> [ ] | ϵ

stmt_list -> stmt_list'
stmt_list' -> stmt stmt_list' | ϵ

stmt -> expr_stmt
        | compound_stmt
        | local_decls
        | if_stmt
        | while_stmt
        | return_stmt
        | break_stmt

expr_stmt -> expr ; | ;

return_stmt -> RETURN return_stmt'
return_stmt' -> ; | expr ;

while_stmt -> WHILE ( expr ) stmt

compound_stmt -> { stmt_list }

if_stmt -> IF ( expr ) stmt if_stmt'
if_stmt' -> ELSE stmt | ϵ

local_decls -> local_decls'
local_decls' -> local_decl local_decls' | ϵ
local_decl -> type_spec IDENT local_decl'
local_decl' -> ; | [ ] ;



expr -> IDENT expr'' expr''''
          | ! expr expr''''
          | - expr expr''''
          | + expr expr''''
          | ( expr ) expr''''
          | BOOL_LIT expr''''
          | INT_LIT expr''''
          | FLOAT_LIT expr''''
          | NEW type_spec [ expr ] expr''''

expr' -> = expr
          | ϵ

expr'' -> [ expr ] expr'
          | = expr
          | ( args )
          | . size
          | ϵ

expr''' -> OR expr
          | EQ expr
          | NE expr
          | LE expr
          | < expr
          | GE expr
          | > expr
          | AND expr
          | + expr
          | - expr
          | * expr
          | / expr
          | % expr
          | & expr

expr'''' -> expr''' expr''''
          | ϵ

args -> arg_list | ϵ
arg_list -> expr arg_list'
arg_list' -> , expr arg_list' | ϵ
