## JWT Authentication in React

- two things we need:
  1. **react-router-dom** for defining routes
  2. **axios** for api calls

### About JWT

#### What JWT is exactly?

- It is a token that only the server can generate, and can contain a payload of data.

#### What's the point of it?

- A JWT payload can contain things like user ID so that when the client sends you a JWT, you
  can **be sure that it is issued by you**, and you can **see to whom it was issued**.

#### Where can it be useful?

- Usually, is `RESTful APIs`, where the server must not use any sort of sessions.

#### How does it differ form using sessions?

- In a typical session flow, the **browser sends a cookie containing a token**, which is **then
  matched at the server** to some data which the server makes use of **to authenticate the user**

- In a JWT flow, **the token itself contains the data**. The server **decodes the token to
  authenticate the user only**. No data stored on the server.

#### What is a typical authentication flow using JWT?

- User credentials sent to `/signin`
- `/signin` returns a JWT (signed with a key)
- JWT is stored is `localStorage`
- JWT is send on every request (to API)
- The server can read the JWT and extract user ID our of it

> JWT contains the encoded form of the alogrithm.data.signature and so if the user tries to
> fiddle with the user ID or any other data held in the jwt, then the jwt signature becomes
> invalid

> JWT is encoded (not encrypted), so any one can read the data component of the jwt (see
> jwt.io for example). Therefore it is recommended not to store any secrets like password in
> the jwt.

> It is also recommended to use an encrypted connection (SSL/TLS) when making the web request
> that contains the jwt because otherwise an attacker can steal the jwt and use it to
> impersonate you.

![img01](https://user-images.githubusercontent.com/34595361/213847475-f4d300c2-2ffc-4489-b9de-9a6fe0edd4c7.jpeg)

### Create the Project

- after creating a react app, these are some more things we need in the app:
  1. **Router** to implement pages, we will use reac-router for this,
  2. **Login Page** which we will get user information and send login request to set
     JWT token.
  3. **Home page** which just be accessible for authenticated users.

### Defining projects routes

- We will use react router for defining routes, so let's install it with following
  command:

```
npm install react-router-dom
```

- We need to set history property to benefit from **react-router-dom** Router component.
  Let's add a helper folder inside our source folder, then add `history.js` inside it:

**history.js**:

```
import { createBrowserHistory } from 'history';

export const history = createBrowserHistory();
```

- After that, let's create a file called **routes.js** in source folder to add our routes:

**routes.js**:

```
import React from "react";
import {Redirect, Switch, Route, Router } from "react-router-dom";

// history
import { history } from './helpers/history';

// pages
import HomePage from "./pages/HomePage"
import LoginPage from "./pages/Login"

function Routes() {
    return (
        <Router history={history}>
            <Switch>
                <Route
                    exact
                    path="/"
                    component={HomePage}
                />
                <Route
                    path="/login"
                    component={LoginPage}
                />
                <Redirect to="/" />
            </Switch>
        </Router>
    );
}

export default Routes;
```

### Updating App.js

- After defining the routes of our project, we need to import our Routers component in App.js.

### Defining Private Route

- We'll create a Route Guard component as an authentication middleware.

- For a more clear explanation, RouteGuard is a route component that you can use instead of
  `react-router-dom` Route component for access control management of pages.

### Step 1: Creating RouteGuard component

**RouteGuard.js**:

```
import React from "react";
import { Route, Redirect } from 'react-router-dom';

const RouteGuard = ({ component: Component, ...rest }) => {

    const flag = !!localStorage.getItem("token");

    return (
        <Route {...rest}
            render={props => (
                flag  ?
                    <Component {...prop} />
                    :
                    <Redirect to={{ pathname: '/login'}} />
            )}
    )
}

export default RouteGuard;
```

### Step 2: Updating our Routes.js file

**route.js**

```
import React from "react";
import {Redirect, Switch, Route, Router} from "react-router-dom";
import RouteGuard from "./component/RouteGuard"

import {history} from './helpers/history';

import HomePage from './pages/HomePage';
import LoginPage from "./pages/Login";

function Routes() {
    return (
        <Router history={history}>
            <Switch>
                <RouteGuard
                    exact
                    path="/"
                    component={HomePage}
                />
                <Route
                    path="/login"
                    component={LoginPage}
                />
                <Redirect to="/" />
            </Switch>
        </Router>
    );
}

export default Routes;
```

### Login Request with "axios"

- We'll use axios in order to make API calls, so lets install axios with npm:

```
npm install axios
```

- Then let's import axios to our login page, and update the handleSumbit function:

**handleSubmit**:

```
const handleSumbit = (email, pass) => {
    // reqres registered sample user
    const loginPayload = {
        email: 'yourmail@gasd.sdf',
        password: 'password'
    }

    axios.post("https://reqres.in/api/login", loginPayload)
        .then(response => {
            const token = response.data.token;
            localStorage.setItem("token", token);

            setAuthToken(token);

            window.location.href = '/'
        })
        .catch(err => console.log(err));
}
```

### Set axios common headers with setAuthToken()

- In order to use JWT on each private request, we need to add them ot the request header as
  expected. Axios has a header common set option, and we'l use that with a helper method
  called setAuthToken().

```
import axios from 'axios';

export const setAuthToken = token => {
    if (token) {
        axios.defaults.header.common["Authorization"] = `Bearer ${token}`;
    }
    else
        delete axios.defaults.headers.common["Authorization"];
}
```

> Note: axios interceptors can be used to do the same operation; especially if you have
> other config, or any kind of condition before every request is sent.

- Finally, we'll need to update App.js as follow to check JWT token right after application
  is created.

```
// check jwt token
    const token = localStorage.getItem("token");
    if (token) {
        setAuthToken(token);
    }
```

- That's it, we just simply implemented JWT authentication in a demo React application. With
  the last operation, our axios request header will include the Bearer token to protect our
  application private API's

-
