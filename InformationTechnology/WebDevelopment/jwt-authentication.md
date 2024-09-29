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
