# Notes related to the Backend Development

## Technologies used:

1. node.js
2. express.js

### Notes

#### To Manage Production and Development backend running in nodejs bare backend:

- Maintain distinct environment files for each environment, such as:

  - `.env.development` for development-specific variables
  - `.env.production` for production-specific variables

- Dynamic Loading Based on Environment
  - Use the `dotenv` package to load the correct .env file depending on the
    environment. In your main entry file, add logic like:

```
const dotenv = require('dotenv');
dotenv.config({path: `.env.${process.env.NODE_ENV}`});
```

- Use the cross-env package to set environment variables in a cross-platform way:

```
"scripts: {
    "dev": "cross-env NODE_ENV=development node app.js",
    "start": "cross-env NODE_ENV=production node app.js"
}"
```

- All all real `.env.*` files to .gitingore

### Prompts
