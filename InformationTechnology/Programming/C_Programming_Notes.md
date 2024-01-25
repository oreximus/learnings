# C Programmings Notes

## Typecasting in C

### Source: [GeeksForGeeks](https://www.geeksforgeeks.org/c-typecasting/)

### Typecasting:

Typecasting in C is the process of converting one data type to another data type by the programmer using the casting operator program design.

In typecasting, the destination data type may be smaller than the source data type when converting the data type to another data type, that's why it is also called narrowing conversion.

**Syntax**:

```
int x;
float y;
y = (float) x;
```

#### Types of Type Casting in C

In C there are two major types to perform type casting:

1. Implicit Type Casting
2. Explicit Type Casting

##### Implicit Type Casting

- Implicit type casting in C is used to convert the data type of any variable without using the actual value that the variable holds.

- It performs the conversions without altering any of the values which are stored in the data variable. Conversion of lower data type to higher data type will occur automatically.

### Switch Statement in C

source: https://www.geeksforgeeks.org/c-switch-statement/

- Switch case statement evaluates a given expression and based on the evaluated value (matching a certain condition), it executes the statements associated with it. Basically, it is used to perform different actions based on different conditions(cases).

    - Switch case statements follows a selection-control mechanism and allow a value to change control of execution.
    - They are a substitute for long **if statements** that compare a variable to several integral values.
    - The switch statement is a multiway branch statement. It provides an easy way to dispatch execution to different parts of code based on the value of the expression.

In C, the switch case statement is used for executing one condition from multiple conditions. It is similar to an if-else-if ladder.

- The switch statement consists of conditional-based cases and a a default case.

### Printing Patterns in C


### Difference between Argument and Parameter in C/C++

**Argument**:

- An **argument** is referred to the values that are passed within a function when the function is called. These values are generally the source of the function that require the arguments during the process of execution.

These values are assigned to the variable in the definition of the function that is called. The type of the values passed in the function is the same as that of the of the variable defined in the function definition. These are also called **Actual arguments** or **Actual Parameters**.

**Example**:

Suppose a sum() function is needed to be called with two numbers to add. These two numbers are referred to as the arguments and are passed to the sum() when it called from somewhere else.

```
// C code to illustrate Arguments

#include <stdio.h>

int sum(int a, int b)
{
    // returning the addition
    return a + b;
}

// Driver code
int main()
{
    int num1 = 10, num2 = 20, res;

    // sum() is called with
    // num1 & num2 as ARGUMENTS.
    res = sum(num1, num2);

    printf("The summation is %d", res);
    return 0;
}
```
**Parameters**:

- The parameter is referred to as the variable that are defined during a function declaration or definition. These variable are used to receive the arguments that are passed during a function call.

These parameters within the function prototype are used during the execution of the function for which it is defined.

These are also called Formal arguments or Formal Parameters.

**Example**: Suppose a Multi() function is needed to be defined to multiply two numbers. These two numbers are referred to as the parameters and are defined while defining the function Multi().

```
// C code to illustrate Parameters

#include <stdio.h>

// Multi: Function definition
// a and b are the PARAMETERS]

int Mult(int a, int b)
{

    // returning the multiplication
    return a*b;
}
```


## Loops

- 3 Different kinds of pyramids to make.
- Even No pyramid and Odd No pyramid to make.
- Using ASCII values to make patterns, i.e. (by %c in the printf(), 64+i, 64+j, where i and j are variable containing integer value from the loop.)
- Using outer loop variable dependency to create patterns, by only changing starting and ending values in the variable it makes the pattern accordingly in the reverse order as well as in the main order.


## Assignment:

1. Right side and Left Side Right Angle Triangle Combination, through loop.

```
*       *
**     **
***   ***
**** ****
**********
```






