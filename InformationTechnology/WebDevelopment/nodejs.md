## NodeJS Notes From Piyush Garg

- Nodejs is developed by **Ryan Dahl** who combined the JavaScript V8 engine and C++ to run the JavaScript
  code outside of the browser.
  Nodejs is a cross-platform, open-source JavaScript runtime environment that can run on Windows, Linux,
  Unix, macOS, and more. Node.js runs on the V8 JavaScript engine, and executes JavaScript code outside a
  web browser.

### Nodejs `npm init` and `package.json` file.

- you can initiate a node project in an existing node project folder by:

```
npm init
```

- after running this command you'll notice a `package.json` file in your node folder.

- we can use package.json file to:
  1. we can make various configuration into this file.
  2. we can install our dependencies using this file.

### Modules, Packages or Modules in NodeJS

- when we divide our code into various modules that's the case of **Modular Programming**.

- for including the modules in nodejs:

```
// for example including a module from current folder
const math = require("./math");
```

- and if you try only to `console.log()` the `math` module, it will return you the empty object, so for
  that you need to export the module in your module defined file which in this case is `math.js`.

```
// exporting modules example, in math.js file
module.exports = add;

// exporting multiple functions
module.exports = {
    add, sub,
}

// exporting by renaming functions
module.exports = {
    addFn: add,
    subFn: sub,
}
```

- You can also destructure the functions name in your code file where you are including the module:

```
// example while require the module
const { add, sub } = require('./math')
```

- we can directly exports the functions by using the exports functions:

```
exports.add = (a, b) => a + b;
exports.sub = (a, b) => a - b;
```

- when we `require` something just by this `require("some_module")` it will search the module in the
  node packages directory, to search module in the current directory do this `require("./some_module)`.

### File handling in NodeJS

- file handling means doing operation on files.

- for file handling we are a nodejs module called `fs`

- creating file using `fs` module
