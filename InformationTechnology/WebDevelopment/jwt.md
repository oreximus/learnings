## JSON Web Tokens

**source**: https://www.npmjs.com/package/jsonwebtoken

### JWT.sign(payload, secretOrPrivateKey, [options, callback])

- (Asynchronous) if callback is supplied, the callback is called with the `err` or the JWT.

- (Synchronous) Returns the JsonWebToken as string.

- `payload` could be an object literal, buffer or string representing valid JSON.

> `exp` or any other claim is only set if the payload is an object literal. Buffer or string payloads are not checked for JSON validity.

> If `payload` is not a buffer or a string, it will be coerced into a string using `JSON.stringify`
