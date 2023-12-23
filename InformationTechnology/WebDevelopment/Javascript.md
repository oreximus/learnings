## Javascript Notes:

### source: https://www.youtube.com/watch?v=W6NZfCO5SIk&t=426s

### What is JavaScript?

- A popular Programming Language.

### What can you do with it?

- We can create:
  - We/Mobile Applications
  - Real-Time Networking Applications
  - Commandline Tools
  - Games

### Where does JavaScript code run?

- JavaScript code runs in Code-Engine which present in the Browser.
  - Like in Firefox: **SpiderMonkey**
  - In Chrome: **v8**

- In 2009 an Engineer named Ryan Dahl took the open-source Javascript Engine in
  Chrome and embedded inside a C++ program and it's known as **Node**, which is
  a C++ program includes a JavaScript engine, with this we can run the
  JavaScript code outside of the browser.

- And with the help of Node(which provides the runtime environment for
  javascript) we can build the Backend of the Web-Application with the help of
  JavaScript.

### JavaScript vs ECMASscript?

- ECMASscript is just a 'specification' and JavaScript a 'Programming Language'
  confirms it's specification.

- We have this orgranization called **ECMA** which is responsible defining
  Standards for ECMASscript specification.

- The first version of ECMASscript specification was released in 1997 and
  starting from year 2015 (ES2015/ES6 was released in 2015, which defined many
  new features of JavaScript) the ECMA is working on annual release of the
  ECMASscript specification.

### Writing JavaScript

- Best practice to place javascript code, at the bottom of the Body Tag.
  - The browser parses the file from top to bottom. Because of this JavaScript
    code can delay the page loading process while it's got busy in executing the
    JavaScript code first.
  - Secondly, the JavaScript code that we are required by the element of website
    so, it's obvious that we need to load the element first in order to
    JavaScript code.
  - In exceptional scenarios, when you're using third party tool then you might
    need to place the JavaScript code in the head section.

- Comments represents by:

```
// this is an example!
```

- We use JavaScript to implement behaviour of the Website.

### Running JavaScript code in Node

- To run JavaScript code with Node:
  - Navigate to the directory location where your JavaScript code is stored and
    run:
  ```
  node yourcodefile.js
  ```
