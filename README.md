# xpl

**xpl**: *eXample Programming Language*.

## About

**xpl** is a tiny toy programming language that is implemented in the course of the [UniCC Parser Generator](https://github.com/phorward/unicc)'s User Manual.
Please check out the [User's Manual](http://phorward.info/download/unicc/unicc.pdf) for implementation details.

## Features

- C-like language [syntax](https://github.com/phorward/xpl/blob/master/xpl.par)
- Arithmetic and conditional expressions
- Dynamically typed
- 3 data-types: integer, float, string
- Simple control structures (conditionals, iterations)
- 6 build-in functions for simple data manipulation routines and input/output facilities: exit(), print(), prompt(), integer(), float(), string() 

## Building

To build `xpl`, you need UniCC and any C-compiler. The provided Makefile should do all the rest for you, when `unicc` is in the PATH.

## Example

The "99 bottles of beer" program implemented in xpl.

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

Run it after building with

```bash
./xpl 99bottles.xpl
```

## Credits

*xpl* is developed and maintained by [Jan Max Meyer](https://github.com/phorward/), Phorward Software Technologies.

## License

xpl is under the WTFPL.
