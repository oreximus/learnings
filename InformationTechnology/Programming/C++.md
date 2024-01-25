# C++ Programming Notes

- It's the same C Programming Language only difference is that it's introduced the OOP's concepts.

- The name of Programming C++, here ++ denotes increment operator and it's kind of obvious that C++ with OPPs is the more featured version of C programming language.

## History

- It's designed By: **Bjarne Stroustrup** in AT&T Bell labs, and First ever released in 1985.

## About the Programming Language Need over C.

- Because C is the procedural programming langauge, we can only perform actions by creating functions in the program and call them accordingly in the needed case.

So, then C++ comes into the play and helps us to create **classes** as we can define a functions only one time in the program with some set of data variables and later it can be called multiple times as being an **object** in the program.

- An **Object** is an instance of a Class. When a class is defined, no memory is allocated but when it is instantiated (i.e. an object is created) memory is allocated.
    - source: https://www.geeksforgeeks.org/c-classes-and-objects/

## Basic Syntax

```
#include <iostream>
using namespace std;
int main(){

    int a,b,c;
    
    cout << "Enter the 2 values:"
    cin >> a >> b;
    count << "sum of" << a << "and" << b << "is" << c;
    
    return 0;
}
```

- iostream **stands for standard input-output stream**. #include iostream declares objects that control reading from and writing to the standard streams.
- using namespace std means that we can use names for objects and variables from the standard library.
- **cout** is an object of output stream that is used to show output on the console.
- **cin** is an object of input stream which used to take input from input stream like files, console, etc.
- \<\< ➝ insertion operation
- \>\> ➝ extraction operator

**Example Syntax with Scope resolution operator**:

```
#include <iostream>
int main(){

    int a,b,c;
    
    std::cout << "Enter the 2 values:"
    std::cin >> a >> b;
    count << "sum of" << a << "and" << b << "is" << c;
    
    return 0;
}
```

- In computer programming, scope is an enclosing context where values and expressions are associated. The scope resolution operator helps to identify and specify the context to which an identifier refers, particularly by specifying a namespace or class.
    - source: https://en.wikipedia.org/wiki/Scope_resolution_operator

**Namespace in C++**

- A namespace is a declarative region that provides a scope to the identifiers (the names of types, functions, variables, etc) inside it. Namespaces are used to organize code into logical groups and to prevent name collisions that can occur especially when your code base includes multiple libraries.
    - source: https://learn.microsoft.com/en-us/cpp/cpp/namespaces-cpp?view=msvc-170

## OOP

- Class
- Object
- Constructor
- Inheritance
- Polymorphism
- Encapsulation
- Data Abstraction

### Class:

Class is a collection of data members and member functions where data member are the variables which can store data and functions which can perform operations on those data members, class is also called user defined data type just like a structures in c.

### Object:

object is an instance of a class which contains or blueprint of a class or basic runtime entity, which contains all the properties and the behaviour of a class. And by the help of that we can access all the properties of a class outside the class.

### Access Modifiers
a way to access to the properties of class through objects!

- public
- protected
- private

## Scope Resolution Operator

- we use this to define the functions associated to some class.

**example**:
```
class Sum{
    private:
    int a,b,c;

    get(){
        cout << "Enter two values: ";
        cin << a << b;
    }

    sum(){
        c = a+b;
    }
    
    show(){
        cout << "\nSum of " << a << " and " << b << " is: " << c;
    }

    friend void oper();
};



int main(){

    
}


```

## Friend Function

- It help us to use the features of a private,public,protected class.

## Encapsulation

- It is a process by which we can wrap hold data and process in a single unit.

## Data Abstraction

- we can show only essential features and hide the remaining

## Constuctor

- It is a special type of function of a class
- It's name same as a class name
- It does not have any return type
- It can't return any kind of value
- It doesn't required calling, it automatically called when we declare an object of a class.

### Types of Constructor:

1. Compiler Defined, default
2. User Defined, default, parameterized, copy
