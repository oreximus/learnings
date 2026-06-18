# TypeScript Handbook Notes

**Date: 2026-06-19**

**Source**: https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html

- First understand this that your existing JavaScript code is also TypeScript code.
- The main benefit of the TypeScript is that it can highlight unexpected behaviour in your code,
  lowering the changes of bugs.

## Types by Inference

- TypeScript knows the JavaScript language and will generate types for you in many cases.
  For example in creating a variable and assigning it to a particular value, TypeScript will
  use the value as its type.

```
let helloWorld = "Hello World";
```

- By understanding how JavaScript works, TypeScript can build a type-system that accepts
  JavaScript code but has types. This offers a type-system without needing to add extra
  characters to make types explicit in your code. That's how TypeScript knows that `helloWorl`
  is a `string` in the above example.

- Visual Studio Code uses TypeScript under the hood to make it easier to work with
  JavaScript.

## Defining Types

- You can use a wide variety of design patterns in JavaScript. However, some design patterns
  make it difficult for types to be iffered automatically (for example, patterns that use
  dynamic programming).
- TypeScript supports an extensive of the JavaScript language, which offeres places for
  you to tell TypeScript what the types should be.
- For example, to create an object with an inferred type which includes `name:`, `string`
  and `id: number`, you can write:

```
const user = {
    name: "Hayes",
    id: 0,
}
```

- You can explicitly describe this object's shape using an `interface` declaration:

```
interface User {
    name: string;
    id: number;
}
```

- If you provide an object that doesn't match the interface you have provided, TypeScript
  will warn you:

```
interface User {
    name: string;
    id: number;
}
```
