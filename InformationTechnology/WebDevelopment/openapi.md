# Notes for OpenAPI documentation integration in my existing express app

- Installing OpenAPI/swagger packages:

- we are using `swagger-autogen` for the OpenAPI documentation.

```
npm i swagger-autogen
```

- Adding scripts to package.json:

```
scripts: {
    swagger-autogen: node swagger-output.js,
    swagger: npm run swagger-autogen && node swagger-server.js
}
```

- creating `swagger-output.js` file:

```
const swaggerAutogen = require('swagger-autogen')();
const doc = {
    info: {
        title: 'Auto Tech News API',
        version: '1.0.0',
        description: 'API documentation for Auto Tech News application'
    },
    host: 'localhost:5000',
    schemes: ['http'],
    securityDefinitions: {
        bearerAuth: {
            type: 'http',
            scheme: 'bearer',
            bearerFormat: 'JWT'
        }
    },
    security: [{ bearerAuth: [] }],
    definitions: {
        User: require('./models/User')
    }
};
const outputFile = './swagger-output.json';
const endpointsFiles = ['./app.js'];
swaggerAutogen(outputFile, endpointsFiles, doc);
```

- creating a `swagger-server.js` file:

```
const express = require('express');
const swaggerUi = require('swagger-ui-express');
const swaggerDocument = require('./swagger-output.json');
const app = express();
app.use('/api-docs', swaggerUi.serve, swaggerUi.setup(swaggerDocument));
app.listen(3001, () => {
    console.log('Swagger docs at http://localhost:3001/api-docs');
});
```

- Updating routes with Response Annotations:

```
// routes/authRoutes.js
// @route   POST /api/auth/register
// @desc    Register a new user
// @access  Public
router.post('/register', register);
// @route   POST /api/auth/login
// @desc    Login user
// @access  Public
router.post('/login', login);
// @route   GET /api/auth/me
// @desc    Get current user
// @access  Private
router.get('/me', protect, getMe);
```

- Secure in Production
- By creating `config/swagger.js`:

```
const swaggerAutogen = require('swagger-autogen')();
const doc = {
    info: {
        title: 'Auto Tech News API',
        version: '1.0.0',
        description: process.env.NODE_ENV === 'production'
            ? 'Internal API documentation'
            : 'API documentation for Auto Tech News'
    },
    host: process.env.SWAGGER_HOST || 'localhost:5000',
    schemes: process.env.NODE_ENV === 'production' ? ['https'] : ['http'],
    securityDefinitions: {
        bearerAuth: {
            type: 'http',
            scheme: 'bearer',
            bearerFormat: 'JWT'
        }
    },
    security: [{ bearerAuth: [] }]
};
const outputFile = './swagger-output.json';
const endpointsFiles = ['./app.js'];
const generateSwagger = async () => {
    await swaggerAutogen(outputFile, endpointsFiles, doc)();
    console.log('Swagger JSON generated');
};
module.exports = { generateSwagger };
```

- Environment-Based Security in app.js:

```
const path = require('path');
const swaggerUi = require('swagger-ui-express');
const { generateSwagger } = require('./config/swagger');
const swaggerEnabled = process.env.SWAGGER_ENABLED === 'true' && process.env.NODE_ENV !== 'production';
// Only generate in non-production
if (process.env.NODE_ENV !== 'production') {
    generateSwagger();
}
// Conditionally mount swagger
if (swaggerEnabled) {
    const swaggerDocument = require('./swagger-output.json');
    app.use('/api-docs', swaggerUi.serve, swaggerUi.setup(swaggerDocument));
}
```

- Adding .env files

```
.env.development:
SWAGGER_ENABLED=true
.env.production:
SWAGGER_ENABLED=false
```

Workflow Summary
| Environment | Command | Access |
|-------------|---------|--------|
| Development | npm run swagger | /api-docs open |
| Staging | Set SWAGGER_ENABLED=true | Via API key |
| Production | Default disabled | Disabled |

- Run npm run swagger-autogen after adding/modifying routes to regenerate the spec.
