**xpl**: *An eXample Programming Language!*

# About

**xpl** is a tiny toy programming language implemented in the course of the manual of the [UniCC Parser Generator](https://github.com/phorward/unicc).
Please check out the [UniCC User's Manual](http://phorward.info/download/unicc/unicc.pdf) for implementation details.

# Features

- C-like syntax
- Typeless language
- Arithmetic and conditional expressions
- Support of integer, floating point and string values
- Simple control structures (conditionals, iterations)
- Variable assignments
- Nested calls to build-in functions with variable arguments
- The functions should provide simple data manipulation routines and input/output facilities

# Compiling

To compile xpl, you need [unicc](https://github.com/phorward/unicc) and any C-compiler. The provided Makefile should do all the rest for you.

# Syntax

The original syntax can be obtained from `xpl.par`.

The syntax described in GDL (Phorward Grammar Definition Language) can be
seen below and was implemented as a parser using [pynetree](https://github.com/phorward/pynetree).

```
%skip           /\\s+/ ;

@REAL           /\\d+\\.\\d*|\\d*\\.\\d+/ ;
@INTEGER        /\\d+/ ;
@STRING         /"[^"]*"/ ;
@IDENT          /\\w+/ ;

program$        :   statement* ;

statement       :   @("if" '(' expression ')' statement ('else' statement)?)
                |   @("while" '(' expression ')' statement)
                |   '{' statement* '}'
                |   expression ';'
                |   ';'
                ;

expression      :   @(expression "==" arith)
                |   @(expression "!=" arith)
                |   @(expression "<" arith)
                |   @(expression ">" arith)
                |   @(expression "<=" arith)
                |   @(expression ">=" arith)
                |   assign
                |   arith
                ;

@assign         :   IDENT "=" expression ;

arith           :   @(arith "+" term)
                |   @(arith "-" term)
                |   term
                ;

term            :   @(term "*" factor)
                |   @(term "/" factor)
                |   factor
                ;

factor          :   @("-" atom)
                |   atom
                ;

atom            :   '(' expression ')'
                |   function_call
                |   IDENT
                |   REAL
                |   INTEGER
                |   STRING
                ;

@function_call  :   IDENT '(' parameter_list? ')'
                ;

parameter_list  :   parameter_list ',' expression
                |   expression
                ;
```

# Example

The "99 bottles of beer" program exposed in xpl:

```c
if( ( bottles = prompt( "Enter number of bottles [default=99]" ) ) == "" )
    bottles = 99;

if( integer( bottles ) <= 0 )
{
    print( "Sorry, but the input '" + bottles + "' is invalid." );
    exit( 1 );
}

while( bottles > 0 )
{
    if( bottles > 1 )
        print( bottles + " bottles of beer on the wall, " +
                bottles + " bottles of beer." );
    else
        print( "One bottle of beer on the wall, one bottle of beer." );

    print( "Take one down, pass it around." );

    if( ( bottles = bottles - 1 ) == 0 )
        print( "No more bottles of beer on the wall." );
    else if( bottles == 1 )
        print( "One more bottle of beer on the wall." );
    else
        print( bottles + " more bottles of beer on the wall." );
}
```

# Author

xpl is developed and maintained by Jan Max Meyer, Phorward Software Technologies.

Some other projects by the author are:

- [unicc](http://unicc.phorward-software.com): The universal LALR(1) parser generator.
- [phorward](http://phorward.phorward-software.com): A free toolkit for parser development, lexical analysis, regular expressions and more.
- [pynetree](http://pynetree.org): A light-weight parsing toolkit written in pure Python.
- [JS/CC](http://jscc.brobston.com): The JavaScript parser generator.

# License

xpl is under the WTFPL.
