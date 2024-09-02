## Global Error Handling Middleware | Error Handling in Express

**source**: https://www.youtube.com/watch?v=WXa1yzLR3hw

- two kinds of errors in the nodejs project:

  1. **Operational Errors**: Operational errors are the problems that we can predict that will
     happen at some point in future. We need to handle them in advance - User trying to access an invalid route. - Inputting invalid data. - Application failed to connect to server. - Request timeout etc.
  2. **Programming Errors**: Programming errors are simply bugs that we programmers, by
     mistake, introduces them in our code. - Trying to read property of an undefined variable - Using await without async. - Accidently using req.query instead of req.body - Passing a number where an object is expected etc.

- implementing the error handling middleware:

```
const express = require("express");

const app = express();

app.use((error, req, res, next) => {
    res.status()
})
```

- `customErrorClass`:

```
class CustomError extends Error{
    constructor(message, statusCode){
        super(message);
        this.statusCode = statusCode;
        this.status = statusCode => 400 && statusCode < 500 ? 'fail' : 'error';

        this.isOperational = true;

        Error.captureStackTrace(this, this.constructor)
    }
}

// const error = new CustomError("some error message", 404)

module.exports = {
    customError;
}
```

**source**: https://www.youtube.com/watch?v=vAH4GRWbAQw

-
