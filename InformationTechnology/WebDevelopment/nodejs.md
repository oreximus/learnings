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

- creating file using `fs` module:

```
const fs = require("fs");

// for creating files synchronously in nodejs
fs.writeFileSync("./test.txt", "Hello World");

// Async
fs.writeFile("./test.txt", "Hello World Async", (err) => {})
```

> it's important to know what to use in the particular task, like Asychronous or Synchronous Jobs should be
> defined according to the need or this can also create the problem of crashing the server.

- reading a file from the local storage:

```
const fs = require("fs");

fs.readFileSync("./file.txt", "utf-8");
console.log(results);
```

- so when we use Asynchronous way to read the file then it'll prompt you an error, because the in this
  way the it does not returning the result values, for that we need to define a callback function with
  `err` and `result` argument.

```
fs.readFile("./file.txt", "utf-8", (err, result) => {
    if (err) {
        console.log("Error", err)
    } else {
        console.log(result);
    }
});
```

- appending the data in a file:

```
// for example appending the date into a file
fs.appendFileSync("./test.txt", new Date().getDate().toLocalString());
```

- copying a file:

```
fs.cpSync('./test.txt', "./copy.txt");
```

- deleting a file:

```
fs.unlinkSync("./copy.txt");
```

- printing out the statistics of a file:

```
console.log(fs.statSync("./test.txt"));
```

- also we can check whether it is a file or directory:

```
console.log(fs.statSync("./test.txt").isFile);
```

- we can also create a directory:

```
fs.mkdirSync("my-docs");
```

- creating directories in a recursive manner:

```
fs.mkdirSync("parent/child1/child2", {recursive: true});
```

### NodeJS Architecture:

![img01](imgs/nodejs01.png)

- in a nutshell we have:
  - request --> go to Node.js server
  - we have event loop in the Node.js server, which is running constantly and checking
    whether there is some operation or task in the queue.
  - from the queue the event loop identifies whether the operation is **Blocking** or
    **Non-Blocking** in the type and accordingly:
  - If **Blocking Operation** then it'll send the operation to the threads to compute
    and once the computation done it'll send back the response.
  - If **Non-Blocking Operation** then it'll will send the response to client by event
    queue.

> by default the threads defined only 4 in the nodejs, so if all threads got busy in doing
> the operation then the upcoming tasks needs to wait until there is some thread available to
> do the tasks, this creates a huge problem while deployed in the server development so be
> aware of this way of using the **Blocking Nature of Operations**

> you can also expand the length of the default thread value in the nodejs project by using
> os module:

```
// expanding the threads in nodejs project
const os = require("os");

// checks the number of VCPUs you have
console.log(os.cpus().length);

// setting the thread size to the length
// of the VCPUs you have

process.env.UV_THREADPOOL_SIZE = OS.cpus().length
```

### Building HTTP Server in NodeJS

- initializing the NodeJS project:

```
npm init
```

- good practice to name the file as `index.js`

- require the `http` module:

```
const http = require("http");
```

- creating a server using the http:

```
const myServer = http.createServer((req, res) => {});
```

- it'll take the callback function where the first object is returning the request related
  stufss and the second one is returning the response.

- sending a response message from the server side:

```
const myServer = http.createServer((req, res) => {
    console.log("New Req Rec.");
    res.end("Hello From Server");
});

myServer.listen(8000, () => console.log("Server Started!"));
```

- above code will make the custom response which will send by the server and the server will
  listen on port 8000 and we can also include the message for ourselves that server is started!

- we'll setup a `start` script in the `package.json` file:

```
// in the script section of package.json file
"start": "node index"
```

- creating a simple HTTP webserver where we can generate the simple Log file for user Requesting
  data info:

```
const http = require("http");
const fs = require("fs");

const myServer = http.createServer((req, res) => {
    const log = `${Date.now()}: New Req Received\n`;
    fs.appendFile("log.txt", log, (err, data) => {
        res.end("Hello From Server Again");
    });
});

myServer.listen(8000, console.log("Server Started!"));
```

- we can also the `req.url` checking the path where user/client is visiting and send the
  response according to that:

```
// rest remains same
const myServer = http.createServer((req, res) => {
    const log = `${Date.now()}: ${req.url} New Req Received\n`;
    fs.appendFile("log.txt", log, (err, data) => {
        switch (req.url) {
            case: "/":
                res.end("Homepage");
                break;
            case: "/about":
                res.end("This is Cool!");
                break;
            default:
                res.end("404 Not Found");
                break;
        }kkkG
    });
});
// rest remains same
```

> always use the Non-Blocking wherever you need to deal the concurrent requests in the server.

## Handling URLs in NodeJS

- structure of the URL:

![img02](imgs/nodejsimg02.png)

- nested path in a URL:

![img03](imgs/nodejsimg03.png)

- query parameters in a URL:

![img04](imgs/nodejsimg04.png)

- URL: Uniform Resource Locator

- Utilization URL parameter and Query strings
  - install a separate package `npm install url`.

```
// rest remains same
const myServer = http.createServer((req, res) => {
    const log = `${Date.now()}: ${req.url} New Req Received\n`;
    const myUrl = url.parse(req.url, true);
    fs.appendFile("log.txt", log, (err, data) => {
        switch (myUrl.pathname) {
            case "/":
                res.end("Homepage");
                break;
            case "/about":
                const username = myUrl.query.myname;
                res.end(`Hi, ${username}`);
                break;
            case "/search":
                const search = myUrl.query.search_query;
                res.end("Here are your results for" + search);
            default:
                res.end("404 Not Found");
                break;
        }
    });
});
// rest remains same
```

- In the above code you can notice that we have used the `url` module to utilize the query
  string in the server logic. Also you need to pass `true` as a second argument of url.parse
  method while defining the variable for url module's url data.

### HTTP METHODS

#### HTTTP GET

- When you want to get some data from the server.

- Whenever you search for a URL in your web browser then by default your browser will make a
  GET request.

- The request will be send to the server the get back the response we need.

#### HTTP POST

- When you want to send and mutate some data in server

#### HTTP PUT

- For example whenever you want to upload a file to the server.

#### HTTP PATCH

- For editing the details in the server.

#### HTTP DELETE

- Whenever you want delete something from the server.

#### Handling HTTP Methods in a nodejs Server:

```
// rest remains same
const myServer = http.createServer((req, res) => {
    const log = `${Date.now()}: ${req.method} ${req.url} New Req Received\n`;
    const myUrl = url.parse(req.url, true);
    fs.appendFile("log.txt", log, (err, data) => {
        switch (myUrl.pathname) {
            case "/":
                res.end("Homepage");
                break;
            case "/about":
                const username = myUrl.query.myname;
                res.end(`Hi, ${username}`);
                break;
            case "/search":
                const search = myUrl.query.search_query;
                res.end("Here are your results for" + search);
            default:
                res.end("404 Not Found");
                break;
        }
    });
});
// rest remains same
```

- In above example in the Log generation we added `req.method` variable which is going to
  provide the request type in the log.

- POST request example on the page:

```
// rest remains same
const myServer = http.createServer((req, res) => {
    const log = `${Date.now()}: ${req.method} ${req.url} New Req Received\n`;
    const myUrl = url.parse(req.url, true);
    fs.appendFile("log.txt", log, (err, data) => {
        switch (myUrl.pathname) {
            case "/":
                res.end("Homepage");
                break;
            case "/about":
                const username = myUrl.query.myname;
                res.end(`Hi, ${username}`);
                break;
            case "/search":
                const search = myUrl.query.search_query;
                res.end("Here are your results for" + search);
            case "/signup":
                if (req.method == "GET") res.end("This is a signup Form");
                else if (req.method === "POST") {
                    // DB Query
                    res.end("Success");
                }
            default:
                res.end("404 Not Found");
                break;
        }
    });
});
// rest remains same
```

- In the above example we have included an extra router `/signup` which demonstrate the
  usage of POST request in the server.

### Getting Started with Express and NodeJS

- first install the Express with:

```
npm install express
```

- setting up express in nodejs server:

```
const express = require("express");

const app = express();

app.get("/", (req, res) => {
    return res.send('Hello From HomePage')
})

app.get('/about', (req, res) => {
    return res.send('Hello From About Page')
})

const myServer = http.createServer(app);
// rest is same
```

- using query parameter directly

```
// rest is the same

app.get("/about", (req, res) => {
    return res.send(`Hello ${req.query.name}`)
})

// rest is the same
```

- for above code the example url be like: `http://localhost:8000/about?name="coolname"`

### How Versioning Works in NodeJS

- Example Version `4.18.2`

  - The version contain three parts:
    1. III (last part) `.2` - changes in this indicates minor fixes (Optional)
    2. II (second part) `.18` - changes in this indicates Recommended Bug Fix or some new features are added.
    3. I (first part) `4` - This is a Major Release or Breaking Update

- `^` this symbol means install all the Recommended and Optional Fixes automatically.
- `~` this means only install optional fixes.
- if there is not any symbol then the version of package should match exactly that we have.
- also there are various combination you can define the package.json file as per your need.

## What is REST API

- There is a term known as **RESTful API** which are some set rules
  or best practices to follow in the server.

- Suppose we have **server** and a **client** and they communicate
  (request and response) to each other by following this RESTful API
  standard.

```mermaid
    flowchart LR
        Server --request--> Client
        Server <--response-- Client
```

- RESTful APIs works on server-client architecture and this means
  that the server and client are individual entity and they should
  not depend on each other.
