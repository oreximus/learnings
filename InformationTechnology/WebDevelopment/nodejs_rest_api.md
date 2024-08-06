## Building REST API's using Node and Express.js

**source**: https://www.youtube.com/watch?v=uNCrMvkPUAE

### What we creating?

- we are creating a REST API - JSON

```

GET /users - List all users

GET /users/1 - Get the user with ID 1

GET /users/2 - Get the user with ID 2

POST /users = Create new user

PATCH /users/1 - Edit the user with ID 1

DELETE /users/1 - Delete the User with ID 1
```

- initialize your npm project:

- in existing project folder

```
npm init
```

- create an `index.js` file

- also install the `express` in your node project:

```
npm install express
```

**index.js**:

```
const express = require("express");

const app = express();
const PORT = 8000;

// routes

app.listen(PORT, () => console.log(`Server Started at PORT: ${PORT}`))
```

- in the `package.json`:

```
// in start script:

"start": "node index.js"
```

- the generate a sample `users` data from mockaroo.com and then copy it to your project.

- then in your `index.js`:

```
// require that the data

const users = require("./users_data.json");

// routes

app.get("/users", (res, req) => {
    return res.json(users);
});
```

- alter all of `/users` routes to `/api/users` for better practices.

- for rendering HTML page for users data:

```
app.get('/users', (req, res) => {
    const html = `
    <ul>
        ${users.map((user) => `<li>${user.first_name}).join("")</li>
    </ul>
    `;
    res.send(html);
})
```

- fetching users data by their IDs:

```
app.get("/api/users/:id", (req, res) => {
    const id = Number(req.params.id);
    const user = users.find((user) => user.id === id);
    return res.json(user);
});
```

- creating a `POST` request for creating a new user:

```
app.post("/api/users", (req, res) => {
    // TODO: create new user with ID
    res.json({ status: "pending"});
});
```

- for editing user details by ID:

```
app.patch("/api/users", (req, res) => {
    // TODO: editing user with ID
    res.json({ status: "pending"});
});
```

- for deleting user details by ID:

```
app.delete("/api/users", (req, res) => {
    // TODO: delete a user with ID
    res.json({ status: "pending"});
})
```

- above you can see that route for GET,POST, PATCH and DELETE are same, so we can merge
  them into one like this:

```
app.route('/api/users/:id')
    .get((req, res) => {
    const id = Number(req.params.id);
    const user = users.find((user) => user.id === id);
        return res.json(user);
    })
    .patch((req, res) => {
        // TODO: editing user with ID
        return res.json({ status: "pending"});
    })
    .delete((req, res) => {
        // TODO: delete a user with ID
        res.json({ status: "pending"});
    })
```
