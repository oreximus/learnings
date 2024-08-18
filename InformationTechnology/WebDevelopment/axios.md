## Making a POST request with Axios

**source**: https://saturncloud.io/blog/axios-post-request-to-send-form-data/

### What is Axios?

- Axios is a promise-based HTTP client for JavaScript that can be used both in the browser and Node.js.
  It is a lightweight and easy-to-use library that provides an easy-to-use interface for making HTTP request
  Axios is built on top of the XML HttpRequest API and the Fetch API.

### Making a POST request with Axios

- Installing axios:

```
npm i axios
```

- post request example, sending form in data in x-www-form-urlencoded:

```
const axios = require("axios");
const querystring = require("querystring");

const formData = {
    name: 'John Doe',
    email: 'johndoe@example.com'
};

axios.post('/sumbit-form', querystring.stringfy(formData), {
    header: {
        'Content-Type': 'application/x-www-form-urlencoded'
    }
})
    .then(function (response) {
        console.log(response.data);
    })
    .catch(function (error) {
        console.log(error);
    })
```

- sending data in JSON format

```
const axios = require('axios');

const data = {
    name: 'John Doe',
    email: 'johndoe@example.com'
};
      alert(JSON.stringify(values, null, 2));
axios.post('/submit-form', data)
    .then(function (response) {
        console.log(response);
    })
    .catch(function (error) {
        console.log(error);
    })
```
