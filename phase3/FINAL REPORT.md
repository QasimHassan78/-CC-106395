#CC 106395: Mini c#

###PROJECT MEMBERS###
StdID | Name
------------ | -------------
**62357** | **Qasim Hassan** 
62352 | Hamza tanveer
## Project Description ##
Our project is related to compiler construction in this we have designed a small mini c compiler first we implement code for our lexical anaylyzer on ubuntu and then we created parser. Our aim was to learn more about how compiler works  

##Sample Language Used ##
Sample language that we used for this project was mini c
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
###Lexical Specification###

the lexical elements of Mini-C. Whitespace is ignored, anything following \ to the end of the line is treated as a comment, and keywords and identifiers are case sensitive. If you use the -d option, YACC will generate a header file y.tab.h containing the appropriate constants for multi-character tokens: yacc -d minic.y This header file will also define YYSTYPE which is used to define semantic stack attributes for the various terminals and non-terminals in the language

Local and global variables, parameters.
Functions, if, while, do``while, return.
=, ?: (ternary), ||, &&, ==, !=, <, >=, +, -, *, ++, -- (post-ops), !, - (unary), [], ()
Integer, character, true and false literals. String literals, with automatic concatenation.
The language it implements is typeless. Everything is a 4 byte signed integer.
Pointer indexing works in increments of 4 bytes, pointer arithmetic is byte-by-byte.

###Grammar###
program -> decl_list

decl_list -> decl decl_list' decl_list' -> decl decl_list' | ϵ decl -> var_decl | fun_decl

var_decl -> type_spec IDENT var_decl' var_decl' -> ; | [ ] ;

type_spec -> VOID | BOOL | INT | FLOAT

fun_decl -> type_spec IDENT ( params ) compound_stmt

params -> param_list | VOID param_list -> param param_list' param_list' -> , param param_list' | ϵ param -> type_spec IDENT param' param' -> [ ] | ϵ

stmt_list -> stmt_list' stmt_list' -> stmt stmt_list' | ϵ

stmt -> expr_stmt | compound_stmt | local_decls | if_stmt | while_stmt | return_stmt | break_stmt

expr_stmt -> expr ; | ;

return_stmt -> RETURN return_stmt' return_stmt' -> ; | expr ;

while_stmt -> WHILE ( expr ) stmt

compound_stmt -> { stmt_list }

if_stmt -> IF ( expr ) stmt if_stmt' if_stmt' -> ELSE stmt | ϵ

local_decls -> local_decls' local_decls' -> local_decl local_decls' | ϵ local_decl -> type_spec IDENT local_decl' local_decl' -> ; | [ ] ;

expr -> IDENT expr'' expr'''' | ! expr expr'''' | - expr expr'''' | + expr expr'''' | ( expr ) expr'''' | BOOL_LIT expr'''' | INT_LIT expr'''' | FLOAT_LIT expr'''' | NEW type_spec [ expr ] expr''''

expr' -> = expr | ϵ

expr'' -> [ expr ] expr' | = expr | ( args ) | . size | ϵ

expr''' -> OR expr | EQ expr | NE expr | LE expr | < expr | GE expr | > expr | AND expr | + expr | - expr | * expr | / expr | % expr | & expr

expr'''' -> expr''' expr'''' | ϵ

args -> arg_list | ϵ arg_list -> expr arg_list' arg_list' -> , expr arg_list' | ϵ


###Approach###

At first these tasks seem to be difficult becasue we had no clue what to do but after our teachers guidance and with the help of internet we started working on the project our project runs with a main bash file once excuted our flex will start checking the test cases that we had put and then generate a lex.yy.c file which gives a detailed view of how flex helped us as a analyzer. Our flex script is divided into three parts first part is the defination part where all the neccessary header files are and then next section contains all the rules. Rules are basically all the valid regular expressions for tokens, keywords and identifiers. After that there is a code section in code section different codes are written that have to be tested.After the lexical phase, the compiler enters the syntax analysis phase. This analysis isdone by a parser. The parser uses the stream of tokens from scanner and assigns themdatatype if they are identifiers.The parser code has a functionality of taking input through a file or through standardinput. This makes it more user-friendly and efficient at the same time.


##Problems Faced##

Following are the problems that we faced 

###Problem 1: We had some issues using ubuntu###

Ubuntu was a issue for us becasue we had no or a little expereince of using ubuntu.But time to time we improved in that 

###Problem 2:Working with a completely different language ###

Working on this new language for us known as mini-c was new but still did it with the help of internet it was not as easy as we thought it would be.

##References##
 [https://docs.huihoo.com/solaris/2.6/802-5880/6i9k05dgj/index.html]
 
 [https://raw.githubusercontent.com/mishal23/mini-c-compiler/master/Parser/Parser%20Report.pdf](https://raw.githubusercontent.com/mishal23/mini-c-compiler)
