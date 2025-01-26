## TypeScript Tutorial for Beginners

**source**: https://www.youtube.com/watch?v=d56mG7DezGs&t=177s

### What is Typscript? Why do we need it? And how is it different from Vanilla JS?

- A programming language to address **shortcomings** of **JavaScript**.

  > `JavaScript` is like a kid without the discipline, who does whatever he/she wants, on the
  > other hand `Typescipt` is like a kid with discipline.

- `Typscript` is built on the top of JavaScript, so every valid JS file is a valid Typescript
  file, but typscript has some of robust features, which allow to create maintained applications
  in less time. - Some of the important features javascript offers: 1. Static typing 2. code completion 3. refactoring 4. shorthand notations

| **Statically-typed**                                    | **Dynamically-type**                                    |
| ------------------------------------------------------- | ------------------------------------------------------- |
| (c++, c#, java)                                         | (python, ruby, javascript)                              |
| int number = 10; // we cannot set it to `number = "a";` | let number = 10; // but we can set it to `number = "a"` |

- The problem with the `Dynamically-Typed` is when we use the Dynamically-Typed variable
  value in a function which expects a `number`, then we have to test the situation with
  various if cases to catch this bug, otherwise our application will behave differently.

- So, this kind of problem is solved in `TypeScript`, TypeScript is essentially JavaScript
  with type checking. With TypeScript we explicitly set the type of our variables upon
  declaration, just like how we code in Statically-typed languages. Then we'll pass our
  code to the TypeScript compiler, and it simply tells us if we are doing something wrong.

- For example:

```
let x: number = 10;

// then we cannot do this:

x = 'a'

// it'll not set the variable value to the string
```

- And all of the above checks are going to happen during our compile time.

### Drawbacks:

- **Compilation**: There is always compilation step involved in TypeScript, because browsers
  don't understand TypeScript code.
  **problem**: - We give our code to typescript compiler, then it compiles and translate our code
  into javascript code, this process is called **Transpilation**. - We have to be a bit **disciplined** for typing code in TypeScript, so for the lazy
  programmers it's a big problem, because this comes in a way to code faster.
  > Prefer JavaScript for Simple Projects and for the Medium to large projects you can use
  > TypeScript.

### Installing Typescript:

- First ensure that you have node installed on your device:

```
npm i -g  typescript
```

- checking the TypeScript version:

```
tsc -v
```

### First TypeScript Program:

- create a empty directory, in your prefered location:

**on your terminal**:

```
mkdir hello-world
```

- open the folder in your favourite IDE.

- create a file `index.ts`:

**example code**:

```
console.log('Hello World');
```

- save and exit the `index.ts` file, and run the following command to compile:

```
tsc index.ts
```

- This will do no effects in our compiled code `index.js` file, because we haven't used
  any TypeScript feature yet.

- Now using the TypeScript feature:

```
let age: number = 20;

// now we can't do this!
age = 'a';
```

- In the above while defing age variable, we have annotate the `age` with `number`, so it
  will be considered as number type variable, and it's value can not set to a string type.

- If we have the above code without the can't do part, it'll generate some output like this:

```
var age = 20;
```

- So, instead of using let here, our TypeScript compiler has compiled the code and changed
  the `let` declaration line to `var`, because TypeScript follows the older version of
  JavaScript which is ECMA Script 5 (ES5).

### Configuring the TypeScript Compiler:

- Initializing TypeScript Project.

```
tsc --init
```

- This will create the `tsconfig.json` configuration file our current directory.

- Example `compilerOptions`:

```
{
  "compilerOptions": {
    /* Visit https://aka.ms/tsconfig to read more about this file */

    /* Projects */
    // "incremental": true,                              /* Save .tsbuildinfo files to allow for incremental compilation of projects. */
    // "composite": true,                                /* Enable constraints that allow a TypeScript project to be used with project references. */
    // "tsBuildInfoFile": "./.tsbuildinfo",              /* Specify the path to .tsbuildinfo incremental compilation file. */
    // "disableSourceOfProjectReferenceRedirect": true,  /* Disable preferring source files instead of declaration files when referencing composite projects. */
    // "disableSolutionSearching": true,                 /* Opt a project out of multi-project reference checking when editing. */
    // "disableReferencedProjectLoad": true,             /* Reduce the number of projects loaded automatically by TypeScript. */

    /* Language and Environment */
    "target": "es2016",                                  /* Set the JavaScript language version for emitted JavaScript and include compatible library declarations. */
    // "lib": [],                                        /* Specify a set of bundled library declaration files that describe the target runtime environment. */
    // "jsx": "preserve",                                /* Specify what JSX code is generated. */
    // "experimentalDecorators": true,                   /* Enable experimental support for legacy experimental decorators. */
    // "emitDecoratorMetadata": true,                    /* Emit design-type metadata for decorated declarations in source files. */
    // "jsxFactory": "",                                 /* Specify the JSX factory function used when targeting React JSX emit, e.g. 'React.createElement' or 'h'. */
    // "jsxFragmentFactory": "",                         /* Specify the JSX Fragment reference used for fragments when targeting React JSX emit e.g. 'React.Fragment' or 'Fragment'. */
    // "jsxImportSource": "",                            /* Specify module specifier used to import the JSX factory functions when using 'jsx: react-jsx*'. */
    // "reactNamespace": "",                             /* Specify the object invoked for 'createElement'. This only applies when targeting 'react' JSX emit. */
    // "noLib": true,                                    /* Disable including any library files, including the default lib.d.ts. */
    // "useDefineForClassFields": true,                  /* Emit ECMAScript-standard-compliant class fields. */
    // "moduleDetection": "auto",                        /* Control what method is used to detect module-format JS files. */

    /* Modules */
    "module": "commonjs",                                /* Specify what module code is generated. */
    // "rootDir": "./",                                  /* Specify the root folder within your source files. */
    // "moduleResolution": "node10",                     /* Specify how TypeScript looks up a file from a given module specifier. */
    // "baseUrl": "./",                                  /* Specify the base directory to resolve non-relative module names. */
    // "paths": {},                                      /* Specify a set of entries that re-map imports to additional lookup locations. */
    // "rootDirs": [],                                   /* Allow multiple folders to be treated as one when resolving modules. */
    // "typeRoots": [],                                  /* Specify multiple folders that act like './node_modules/@types'. */
    // "types": [],                                      /* Specify type package names to be included without being referenced in a source file. */
    // "allowUmdGlobalAccess": true,                     /* Allow accessing UMD globals from modules. */
    // "moduleSuffixes": [],                             /* List of file name suffixes to search when resolving a module. */
    // "allowImportingTsExtensions": true,               /* Allow imports to include TypeScript file extensions. Requires '--moduleResolution bundler' and either '--noEmit' or '--emitDeclarationOnly' to be set. */
    // "rewriteRelativeImportExtensions": true,          /* Rewrite '.ts', '.tsx', '.mts', and '.cts' file extensions in relative import paths to their JavaScript equivalent in output files. */
    // "resolvePackageJsonExports": true,                /* Use the package.json 'exports' field when resolving package imports. */
    // "resolvePackageJsonImports": true,                /* Use the package.json 'imports' field when resolving imports. */
    // "customConditions": [],                           /* Conditions to set in addition to the resolver-specific defaults when resolving imports. */
    // "noUncheckedSideEffectImports": true,             /* Check side effect imports. */
    // "resolveJsonModule": true,                        /* Enable importing .json files. */
    // "allowArbitraryExtensions": true,                 /* Enable importing files with any extension, provided a declaration file is present. */
    // "noResolve": true,                                /* Disallow 'import's, 'require's or '<reference>'s from expanding the number of files TypeScript should add to a project. */

    /* JavaScript Support */
    // "allowJs": true,                                  /* Allow JavaScript files to be a part of your program. Use the 'checkJS' option to get errors from these files. */
    // "checkJs": true,                                  /* Enable error reporting in type-checked JavaScript files. */
    // "maxNodeModuleJsDepth": 1,                        /* Specify the maximum folder depth used for checking JavaScript files from 'node_modules'. Only applicable with 'allowJs'. */

    /* Emit */
    // "declaration": true,                              /* Generate .d.ts files from TypeScript and JavaScript files in your project. */
    // "declarationMap": true,                           /* Create sourcemaps for d.ts files. */
    // "emitDeclarationOnly": true,                      /* Only output d.ts files and not JavaScript files. */
    // "sourceMap": true,                                /* Create source map files for emitted JavaScript files. */
    // "inlineSourceMap": true,                          /* Include sourcemap files inside the emitted JavaScript. */
    // "noEmit": true,                                   /* Disable emitting files from a compilation. */
    // "outFile": "./",                                  /* Specify a file that bundles all outputs into one JavaScript file. If 'declaration' is true, also designates a file that bundles all .d.ts output. */
    // "outDir": "./",                                   /* Specify an output folder for all emitted files. */
    // "removeComments": true,                           /* Disable emitting comments. */
    // "importHelpers": true,                            /* Allow importing helper functions from tslib once per project, instead of including them per-file. */
    // "downlevelIteration": true,                       /* Emit more compliant, but verbose and less performant JavaScript for iteration. */
    // "sourceRoot": "",                                 /* Specify the root path for debuggers to find the reference source code. */
    // "mapRoot": "",                                    /* Specify the location where debugger should locate map files instead of generated locations. */
    // "inlineSources": true,                            /* Include source code in the sourcemaps inside the emitted JavaScript. */
    // "emitBOM": true,                                  /* Emit a UTF-8 Byte Order Mark (BOM) in the beginning of output files. */
    // "newLine": "crlf",                                /* Set the newline character for emitting files. */
    // "stripInternal": true,                            /* Disable emitting declarations that have '@internal' in their JSDoc comments. */
    // "noEmitHelpers": true,                            /* Disable generating custom helper functions like '__extends' in compiled output. */
    // "noEmitOnError": true,                            /* Disable emitting files if any type checking errors are reported. */
    // "preserveConstEnums": true,                       /* Disable erasing 'const enum' declarations in generated code. */
    // "declarationDir": "./",                           /* Specify the output directory for generated declaration files. */

    /* Interop Constraints */
    // "isolatedModules": true,                          /* Ensure that each file can be safely transpiled without relying on other imports. */
    // "verbatimModuleSyntax": true,                     /* Do not transform or elide any imports or exports not marked as type-only, ensuring they are written in the output file's format based on the 'module' setting. */
    // "isolatedDeclarations": true,                     /* Require sufficient annotation on exports so other tools can trivially generate declaration files. */
    // "allowSyntheticDefaultImports": true,             /* Allow 'import x from y' when a module doesn't have a default export. */
    "esModuleInterop": true,                             /* Emit additional JavaScript to ease support for importing CommonJS modules. This enables 'allowSyntheticDefaultImports' for type compatibility. */
    // "preserveSymlinks": true,                         /* Disable resolving symlinks to their realpath. This correlates to the same flag in node. */
    "forceConsistentCasingInFileNames": true,            /* Ensure that casing is correct in imports. */

    /* Type Checking */
    "strict": true,                                      /* Enable all strict type-checking options. */
    // "noImplicitAny": true,                            /* Enable error reporting for expressions and declarations with an implied 'any' type. */
    // "strictNullChecks": true,                         /* When type checking, take into account 'null' and 'undefined'. */
    // "strictFunctionTypes": true,                      /* When assigning functions, check to ensure parameters and the return values are subtype-compatible. */
    // "strictBindCallApply": true,                      /* Check that the arguments for 'bind', 'call', and 'apply' methods match the original function. */
    // "strictPropertyInitialization": true,             /* Check for class properties that are declared but not set in the constructor. */
    // "strictBuiltinIteratorReturn": true,              /* Built-in iterators are instantiated with a 'TReturn' type of 'undefined' instead of 'any'. */
    // "noImplicitThis": true,                           /* Enable error reporting when 'this' is given the type 'any'. */
    // "useUnknownInCatchVariables": true,               /* Default catch clause variables as 'unknown' instead of 'any'. */
    // "alwaysStrict": true,                             /* Ensure 'use strict' is always emitted. */
    // "noUnusedLocals": true,                           /* Enable error reporting when local variables aren't read. */
    // "noUnusedParameters": true,                       /* Raise an error when a function parameter isn't read. */
    // "exactOptionalPropertyTypes": true,               /* Interpret optional property types as written, rather than adding 'undefined'. */
    // "noImplicitReturns": true,                        /* Enable error reporting for codepaths that do not explicitly return in a function. */
    // "noFallthroughCasesInSwitch": true,               /* Enable error reporting for fallthrough cases in switch statements. */
    // "noUncheckedIndexedAccess": true,                 /* Add 'undefined' to a type when accessed using an index. */
    // "noImplicitOverride": true,                       /* Ensure overriding members in derived classes are marked with an override modifier. */
    // "noPropertyAccessFromIndexSignature": true,       /* Enforces using indexed accessors for keys declared using an indexed type. */
    // "allowUnusedLabels": true,                        /* Disable error reporting for unused labels. */
    // "allowUnreachableCode": true,                     /* Disable error reporting for unreachable code. */

    /* Completeness */
    // "skipDefaultLibCheck": true,                      /* Skip type checking .d.ts files that are included with TypeScript. */
    "skipLibCheck": true                                 /* Skip type checking all .d.ts files. */
  }
}

```

- Some important settings:

  - `target`: this specify the version of JavaScript, that the TypeScript compiler is
    going to generate.
  - In the `Modules` section we have a setting called `rootDir`, which contains source code
    path, you can modify this set your source path.
  - In the `Emit` section we have a setting called `outDir`, which will contains our
    JavaScript files, we'll set it's value to `./dist`, so all our JavaScript code will
    stored in the `dist` folder.
  - In the `Emit` section there also a setting called `removeComments`, setting it's value
    to be `true`, makes our JavaScript code looks smaller by removing unneccesary comments.
  - Another important setting in `Emit` section is `noEmitOnError`, setting it's value
    to true makes TypeScript compiler to not to generate any JavaScript files if it found
    any errors in the code.

- Now we can directly compile our TypeScript code with:

```
tsc
```

### Debugging TypeScript Applications:

- Going again in the `tsconfig.json` file and enable the `sourceMap` feature in the Emit
  section.

- `**sourceMap**` is a file which specifies how each line of our TypeScript code maps to the
  generated JavaScript code.

- after doing the setting, running `tsc` again, will produce a `index.js.map` file in our
  `dist` folder, which specifies how our TypeScipt code maps to the JavaScript code.

- then go to code-editor, in my case in `vscode`, create modify the code in `index.ts`:

```
let age: number = 20;
if (age < 50)
    age += 10;
```

- and create a breakpoint on line 1, then go to the `debug panel` and `create launch.json file`.

- select `node.js` and this will create new file in your project named as: `launch.json`.

- this file has the configuration which tells vscode how to debug the application.

```
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [

        {
            "type": "node",
            "request": "launch",
            "name": "Launch Program",
            "skipFiles": [
                "<node_internals>/**"
            ],
            "program": "${workspaceFolder}/index.ts",
            "outFiles": [
                "${workspaceFolder}/**/*.js"
            ]
        }
    ]
}
```

- we'll one more to the above config, `"preLaunchTask": "tsc: build - tsconfig.json"`:

```
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [

        {
            "type": "node",
            "request": "launch",
            "name": "Launch Program",
            "skipFiles": [
                "<node_internals>/**"
            ],
            "program": "${workspaceFolder}/index.ts",
            "preLaunchTask": "tsc: build - tsconfig.json",
            "outFiles": [
                "${workspaceFolder}/**/*.js"
            ]
        }
    ]
}
```

- then go back to your `index.ts` file and open the debug panel, and start debugging by pressing `F5`.

- you can add expressions in the debugging panel's watch section, like we can watch
  `age` variable, then re-run the debugger, and press `F10` to see the value of `age`
  variable on each line.

### Fundamentals:

- Concepts:
  1. The any type
  2. Arrays
  3. Tuples
  4. Enums
  5. Functions
  6. Objects

#### Built-in Types:

- Builtin-Types in JavaScript and TypeScript:

  - **JavaScript**:
    - number
    - string
    - boolean
    - null
    - undefined
    - object
  - **TypeScript**:
    - any
    - unknown
    - never
    - enum
    - tuple

- Exploring a bit about the primitive types in TypeScript.

- In `index.ts`, replace the code with:

```
let sales: number = 123_456_789;
let course: string = 'TypeScript';
let is_published: boolean = true;
```

#### The any Type:

- Defining some variable without the value, will be assumed as `any` type variable in
  TypeScript.

- The any type variable can have any type of value, this allows us to loose the Type defined
  functionality in variable declaration in TypeScript.

> Best practice is to avoid using the `any` type variable declaration as much as possible.

```
// for example we if create a
// function

function render(document) {
    console.log(document);
}
```

- the above function declaration will give the compilation error that `Parameter 'document; 
implicitly has an 'any' type`

- to fix this we can annotate the value with `any`.

**for example**:

```
function render(document: any){
    console.log(document);
}
```

- other way is changing some of the settings in our `tsconfig.js` file:

**Under Type Checking section**:

```
"noImplicitAny": true,
```

> Better not to config this setting or you'll loose the major benefits of TypeScript.

#### Arrays:

- In JavaScript we declare arrays like this:

```
let numbers = [1,2,3];
```

- But if we change the values of array like this:

```
let numbers = [1,2,'3'];
```

- On third element, It'll produce an error, this is where TypeScript comes into play!

- Array declaration in TypeScript:

```
let numbers: number[] = [1,2,3];
```

- the type annotation will make sure that every element in this list is a number.

- if we define an empty array:

```
let numbers = []
```

- This will be considered as `any` type array in TypeScript, which we should avoid.

- do this instead:

```
let numbers: number[] = [];
```

- another benefit of TypeScript is code completion or IntelliSense.

- for example:

```
// do this will get all the
// number method for the object

numbers.forEach(n => n.)

```

- suggests you the methods like:
  - toExponential
  - toFixed
  - toLocationString
  - toPrecision
  - toString
  - valueOf

#### Tuples

- TypeScript has a new type called tuples, which is a fixed length array, where each element
  has particular type. We often use them when working with the pair of values.

```
let user: [number, string] = [1, 'Cool', 0]
```

- this will give the error:
  `Type '[number, string, number]' is not assignable to type '[number, string]'.`

- we can only do this:

```
let user: [number, string] = [1, 'Cool']
```

- so if you access the elements, based on type declaration you'll have all the methods
  associated to them.

- Run `tsc` on your terminal after saving the `index.ts` file:

- and you'll see the standard js array in `index.js` file:

```
"use strict";
let user = [1, 'Cool'];
//# sourceMappingURL=index.js.map
```

> Tuple is fixed length array, where each element has a particular type. As a best practice
> restrict your tuple to only two values, because more than that is going to make your
> code a bit hard to understand.
