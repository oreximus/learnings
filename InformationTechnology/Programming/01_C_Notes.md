# C Programming Notes from "The C Programming Language"

## fareheit to celcius scale table program

- the two lines are a comment, which in this case explains briefly what the program does. Any character between /* and */ are ignored by the compiler; they may be used freely to make a program earier to understand. Comments may appear anywhere a blank or tab or newline can.

```
/* print Farenheit-Celcius table
    for fahr = 0, 20, ..., 300 */
```

- In C, all variables must be declared before they are used, usually at the beginning of the function before any executable statements. A declaration announces the properties of variables; it consists of a type name annd a list of variables, such as

```
    int fahr, celcius;
    int lower, upper, step;
```

- the type int means that the variables listed are integers, by contrast with float which means floating point i.e. numbers that may have a fractional part.

- The range of both *int* and *float* depends on the machine you are using; 16-bit ints, which lie between -32768 and +32767, are common, as are 32-bit ints. A *float* number is typically a 32-bit quantity, with at least six significant digits and magnitude generally between about 10<sup>-38</sup> and 10<sup>+38</sup>.

- C provides several other basic data types besides *int* and *float*, including:

1. char         character -- a single byte
2. short        short integer
3. long         long integer
4. double       double-precision floating point

- The size of these objects are also machine-dependent. There are also *arrays*, *structure*, and *unions* of these basic types, pointers to them, and *functions* that return them, all of which we will meet in due course.

- Computation in the temperature conversion program begins with the assignment statements which set the variables to their initial values. Individual statements are terminated by semicolons.

```
    lower = 0;
    upper = 300;
    step = 20;
    fahr = lower;
```

- Each line of the table is computed the same way, so we use a loop that repeats once per output line; this is the purpose of the while loop

```
    while (fahr <= upper){
        ...
    }
```

The while loop operates as follows: the condition in parenthesis is tested. if it is true (fahr is less than or equal to upper), the body of the loop (the three statements enclosed in braces) is executed. Then the condition is re-tested, and if true, the body is executed again.

- When the test becomes false (fahr execeeds upper) the loop ends, and execution contines at the statement that follows the loop. There is no f