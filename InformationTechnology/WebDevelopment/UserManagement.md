# User Management System – Nodejs, Express, MySQL & Express-Handlebars

**source**: https://www.youtube.com/watch?v=1aXZQcG2Y6I

- create a folder `User management tutorial` or anything you like:

- and then `npm init`

- `npm install` to install all the dependency.

- `npm install express dotenv express-handlebars body-parser mysql`

- `npm install --save-dev nodemon`

- then open the project in your code editor.

- add the line in the `scripts` in the package.json file:

```
"start": "nodemon app.js"
```

- create a `app.js` file:

```
const express = require('express');

const app = express();
const port = process.env.PORT || 5000;

app.listen(port, () => console.log(`Listenting on port ${port}`))
```

- then `npm start`, will make the server and listening on port 5000

```
const express = require('express');
const exphbs = require('express-handlebars');
const bodyParser = require('body-parser');
const mysql = require('mysql');

require('dotenv').config();

const app = express();
const port = process.env.PORT || 5000;

// Parsing middleware
// Parse application/x-www-form-urlencoded

app.use(bodyParser.urlencoded({ extended: false}));

// Parse application/json
app.use(bodyParser.json());

// Static files
app.use(express.static('public'));

// Template Engine
app.engine('hbs', exphbs( {extname: '.hbs' }));
app.set('view engine', 'hbs');

// Router
app.get('', (req, res) => {
    res.render('home');
});

app.listen(port, () => console.log(`Listenting on port ${port}`))

```

> Use documentation for further explanation of the topics.

- create a new folder called `public/css` and create new file named `main.css`

- after setting up all the code above, just `npm start` again, and you'll notice we now not get that `Cannot GET` stuff.

- setup main layout.

  - in the `main.hbs` file, write a html file.
  - in the body section:
    ```
    {{{body}}}
    ```

- the page you don't see any changes because we don't have anything there but if you see in the source of that page you'll get the HTML stuffs that we've have just coded.

- If you put anything there you'll get the rendered stuff on the `/` page.

- using css, js and icons of bootstrap.

-
