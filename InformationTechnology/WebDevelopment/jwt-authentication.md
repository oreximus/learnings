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

## Adding JWT Authentication to React

- JSON Web Token (JWT) authentication is a method if securely authenticating users and allowing
  them to access protected resources or application. It's a popular and widely used method of
  web authentication as it allows for easy and secure user authentication without the need for
  the server to maintain a session state.

- In this process, the server generates a signed JWT and sends it to the client. The client
  then includes this token in subsequent requests to the server to authenticate themselves.
  The JWT is usually stored in the browser's localStorage and sent as part of the request's
  headers.

## What is JWT Authentication?

1. `The header`: consists of two parts - the token type, which is JWT, and a signing alogrithm,
   such as HMAC-SHA256 or RSA

2. `The payload`: contains the claims - in other words, the statements about an entity
   (typically, the user) and additional data

3. `The signature`: used to verify the JWT's integrity

- To authenticate a client using JWT, the server first generates a signed JWT and sends it
  to the client. The client then includes the JWT in the header (usually the authorization header)
  of subsequent requests to the server.

- The server then decodes the JWT and verifies the signature to ensure that a trusted party
  sent it. If the signature is valid, the server can then use the information contained in the
  JWT to authenticate the client and authorize their access to specific resources. The diagram
  below shows a standard JWT authentication flow:

![img02](https://clerk.com/_next/image?url=%2F_next%2Fstatic%2Fmedia%2F_blog%2Fadding-jwt-authentication-to-react%2Fce92a5f67e79db690f9dffa38d625decebf8da3e-2025x1178.png&w=828&q=75)

### Advantages and Downsides of Using JWT

1. `JWT authentication is stateless`: A JWT contains all the information regarding the user's
   identity and authentication, including the claims. This can be more efficient than storing
   session information on the server as it reduces the amount of data that needs to be stored
   and retrieved for each request.

2. `Create anywhere`: Another advantage of JWT authentication is that the token can be
   generated from anywhere, including external services or third-party applications. This
   allows for flexibility in terms of where and how the token is generated, which can be useful
   in a microservices architecture where different services may need to authenticate users.

3. `Fine-grained access control`: JWT can contain information about the user's role and
   permissions in the form of claims. This gives the application developers a lot of control
   over what actions a user is allowed to take.

- However, there are also some disadvantages to using JWT authentication:

1. `Hard to invalidate`: Invalidating JWTs is only possible if you maintain a list on a
   shared database, which introduces additional overhead. The database is necessary because
   if you need to revoke a token or if a user's permissions change, the server won't otherwise
   be able to determine the status of the token and might give access when it shouldn't. If
   the JWTs you're using are long-lived -- in other words, they have a very long (or no)
   expiration time specified - it becomes even more important that they're stored in an
   accessible database.

2. `Size and security concerns`: JWTs can sometimes contain unnecessary information that
   might be useless for the application and, at the same time, make the token larger and more
   cumbersome to work with. If the JWT is unencrypted, it can also end up revealing too much
   about the user.

### Are Cookies Better that JWT?

- To start with, you can create session-based cookies, which automatically expire after the user
  session is closed, or you can easily set an expiration time for a cookie, which give more control
  over session invalidation. You can also use HttpOnly cookies to prevent JavaScript from accessing
  the cookie information.

- However, it's important to note that cookie come with their own flaws. Specifically, as the cookie
  data is stored on the server and the cookie identifier is stored on the client, they're not
  entirely stateless like JWTs. This means that the server needs to store and retrieve the cookie
  data for each request, which would be additional overhead to the authentication process and slow
  down the application's performance, especially if the number of concurrent users increases.

- They're also not idealy for non-browser-based applicaitons, such as mobile and desktop
  applications. Additionally, cookies can be more vulnerable to certain attacks, such as
  cross-site scripting (XSS) and cross-site request forgery (CSRF)

- Now that we've covered the advantages and some of the potential challenges of JWT authentication,
  let's see the process in action. In the following section, you'll see how to implement JWT
  authentication in your React application.

### Implementing JWT Authentication in Your React Applications
