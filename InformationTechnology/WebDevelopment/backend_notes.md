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

#### Sequelize installation and basics:

- To install sequilize:

```
npm install --save sequelize
```

- Install the required database npm package (i.e. MySQL):

```
npm install --save mysql2
```

#### Maintaining/Managing Logs with `winston`:

- Example with winston:

```
const winston = require("winston");
const logger = winston.createLogger({
    level: 'info',
    format: winston.format.combine(
    winston.format.timestamp(),
    winston.format.json()
    ),
    transport: [
     new winston.transports.Console(),
     new winston.transports.File({ filename: 'app.log'})
    ]
});
logger.info('Server started', {port: 3000})
```

- Use logs levels appropriately:
  - Categorize logs by severity: `error`, `warn`, `info`, `debug`, etc.
    - `error`: Critical failures
    - `warn`: Non-fatal issues
    - `info`: Key events (startup, shutdown, user actions)
    - `debug`: Detailed diagnostic information
  - Log Rotation and Retention:
    - Implement log rotation to prevent log files from growing indefinitely.
      Use tools or transport (like `winston-daily-rotate-file`) to create new
      log files periodically and remove old ones.
    - Example with Winston:
    ```
    const { transport } = require("winston");
    require('winston-daily-rotate-file');
    const fileRotateTransport = new transports.DailyRotateFile({
        filename: 'app-%DATE%.log',
        datePattern: 'YYYY-MM-DD',
        maxFiles: '14d',
        maxSize: '20m'
    })
    ```

### Prompts
