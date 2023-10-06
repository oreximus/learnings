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
