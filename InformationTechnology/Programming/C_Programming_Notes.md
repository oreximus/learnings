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
*        *
**      **
***    ***
****  ****
**********
```

## Array 

- Array is a collection of similar type of data or homegeneuos element in a continuos memory blocks, In that each and every blocks can be uniquely access through indexing, which always starts from 0 to size-1. 

## Pointers

- **Pointers** are one of the core components of the C Programming language. A pointer can be used to store the **memory address** of other variable, functions, or even other pointers.

- The use of pointers allows low-level memory access, dynamic memory allocation, and many other functionalities in C.

### What is a Pointer in C?

`A pointer is defined as a derived data type that can store the address of other C variables or a memory location. We can access and manipulate the data stored in that memory location using pointers.`

- As the pointers in C store the memory addresses, their size is independent of the type of data they are pointing to. This size of pointers in C only depends on the system architecture.

### Sytax of C Pointers

- The syntax of pointers is similar to the variable declaration in C, but we use the `(*) dereferencing operator` in the pointer declaration.

```
datatype * ptr;
```

where
- **ptr** is the name of the pointer.
- **datatype** is the type of data it is pointing to.

The above syntax is used to define a pointer to a variable. We can also define pointers to functions, structures, etc.

### How to use Pointers?

- The use of pointers in C can be divided into three steps:

1. **Pointer Declaration**
2. **Pointer Initialization**
3. **Pointer Dereferencing**

#### 1. Pointer Declaration

In pointer declaration, we only declare the pointer but do not initialize it. To declare a pointer, we use the `(*) dereference operator` before its name.

**Example**:

```
int *ptr;
```

The pointer declared here will point to some random memory address as it is not initialized. Such pointers are called wild pointers.

#### 2. Pointer Initialization

- Pointer initialization is the process where we assign some initial value to the pointer variable. We generally use the `(&) addressof operator` to get the memory address of a variable and then store it in the pointer variable.

**Example**:

```
int var = 10;
int * ptr;
ptr = &var;
```

We can also declare and initialize the pointer in a single step. This method is called `pointer definition` as the pointer is declared and initialized at the same time.

**Example**:

```
int *ptr = &var;
```

`**Note**: It is recommended that the pointers should always be initialized to some value before starting using it. Otherwise, it may lead to number of errors.`

#### 3. Pointer Dereferencing

- Dereferencing a pointer is the process of accessing the value stored in the memory address specified in the pointer. We use the same `(*) dereferencing operator` that we used in the pointer declaration.

#### C Pointer Example:

```
#include <stdio.h>

void cool()
{
    int var = 10;
    
    // declare pointer variable
    int* ptr;

    // note that data type of ptr and var must be same
    ptr = &var;

    // assign the address of a variable to a pointer
    printf("Value at ptr = %p \n", ptr);
    printf("Value at var = %d \n", var);
    printf("Value at *ptr = %d \n", *ptr);
}

int main()
{
    cool();
    return 0;
}
```

### C Dynamic Memory Allocation

Sometimes the size of the array we declared is insufficient. To solve this issue, we can allocate memory manually during run-time. This is known as dynamic memory allocation in C Programming.

To allocate memory dynamically, library functions are `malloc()`, `calloc()`, `realloc`, and `free()` are used. These functions are defined in the `<stdlib>` header file.

#### C malloc()

- The name "malloc" stands for memory allocation.

- The `malloc()` function reserves a block of memory of the specified number of bytes. And, it returns a `pointer` of `void` which can be casted into pointers of any form.

- `malloc()` is a library function that allows C to allocate memory dynamically from the heap.

- The heap is an area of memory where something is stored. malloc() is part of stdlib.

**Syntax of malloc()**

```
ptr = (castType*) malloc(size)
```

**Example**:

```
ptr = (float*) malloc(100 * sizeof(float));
```
- The above statement allocates 400 bytes of memory, It's because the size of `float` is 4 bytes. And, the pointer `ptr` holds the address of the first byte in the allocated memory.

- The expresson results in a `NULL` pointer if the memory cannot be allocated.

