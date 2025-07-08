# Typescripts Notes:

**source**: https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html

- JavaScript provides language primitives like `string` and `number`, but it doesn't check that
  you've consistently assigned these. TypeScript does.

- The main benefit of TypeScript is that it can highlight unexpected behaviour in your code,
  lowering the chance of bugs.

### Types by Inference:

- Typescript knows that JavaScript language and will generate types for you in many cases. For
  example in creating a variable and assigning it to a particular value, TypeScript will use the value
  as its type.

```
let helloWorld = "Hello World";
```

- By understanding how JavaScript works, TypeScript can build a type-system that accepts JavaScript
  code but has types. This offers a type-system without needing to add extra characters to make
  types explicit in your code.

- That's how TypeScript knows that `helloWorld` is a `string` in the above example.

### Defining Types:

- You can use a wide variety of design patterns in JavaScript. However, some design patterns make it
  difficult for types to be inferred automatically (for example, patterns that use dynamic programming).
  To cover these cases, TypeScript supports an extension of the JavaScript language, which offers places
  for you to tell TypeScript what the types should be.

- For example, to create an object with an inferred type which include `name: string` and `id: number`,
  you can write:

```
const user = {
    name: "Hayes",
    id: 0,
}
```

- You can explicitlt describe this object's shape using an `interface` declaration:

```
interface User {
    name: string;
    id: number;
}
```

- You can then declare that a JavaScript object conforms to the shape of your new `interface` by
  using syntax like `:` `TypeName` after a variable declaration:

```
const user: User = {
    name: "Hayes",
    id: 0,
}
```

- If you provide an object that doesn't match the interface you have provided, Typescript will warn
  you:
