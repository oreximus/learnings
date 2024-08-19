## JOI Validation Schema to validate request body | Node JS API Authentication

**source**: https://www.youtube.com/watch?v=u9kxYilQ9l8&list=PLw5h0DiJ-9PAQ61Pg47RYgQvJ8GAS7sCu

- create a separate schema file `validation_schema.js`:

```
const Joi = require("@hapi/joi")

const authSchema = Joi.object({
    email: Joi.string().email().lowercase().required(),
    password: Joi.string().min(2).required(),
})

module.exports = {
    authSchema,
}
```

- using the schema in our route:

```
// require the authSchema
const { authSchema } = require('../helpers/validation_schema.js')

const result = await authSchema.validateAsync(req.body)
console.log(result)
```

- modifying the response codes in response:

- In `authRoute` file:

```
// if the error occurs in the response
// authentication

if (error.isJoi == true) error.status = 422;

```
