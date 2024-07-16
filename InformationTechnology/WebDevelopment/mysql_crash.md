## MySQL Notes

**source**: https://www.youtube.com/watch?v=9ylj9NR0Lcg

## MySQL Crash Course

### What is MySQL

- Popular **open source relational database management
  system**
- Uses the **SQL** (Structured Query Language).
- A Leading database for web applications
- Used for small apps to large enterprise apps
- Used with mutiple languages (PHP, Node, Python, C#, etc)
- Cross platform (can install on any platform, windows,
  linux, macOS etc.)

### Relational Database

- Based on **"relational model"** of data.
- Virtually all RDBMS use SQL to manage them
- Uses **"tables"** with **"columns"** and **"rows"**
- Tables can relate to eachother by keys.

### Tables and Data Types

![img01](imgs/img01.png)

### Table Relationships

![img02](imgs/img02.png)

- In database we have tables and we can have the
  relationships between them.
- there are primary key in tables which are unique
  identifiers.
- and we can also create `foreign keys` in
  tables to make relationship with the other table.

### Installation and Environment!

#### Local:

- Terminal/GUI Install - Standalone Server
- XAMPP, MAMP, WAMP (Usually used for local
  deelopment)

#### Production:

- Terminal installation via Linux package manager
- Server software (CPanel, etc.)

### Management Tools

- Terminal / Command Line / Shell
- Desktop Tools - MySQL Workbench, etc.
- Web Based Tools - PHPMyAdmin, etc.

### Practical Portion:

#### On Terminal

- you can check MySQL version with:

```
mysql --version
```

- connecting MySQL database with root user:

```
mysql -u root -p
```

- creating user for our operations:

```
// SQL command for creating user
CREATE USER 'user'@'localhost' IDENTIFIED BY 'password';
```

> Capital letters in SQL Command is just a Common
> convention while typing commands.

- we can see the created user is just by:

```
SELECT user, host FROM mysql.user;
```

- providing privileges to the created user:

```
GRANT ALL PRIVILEGES ON * . * TO 'user'@'localhost';
```

- Flush privileges to clear the grant table.

```
FLUSH PRIVILEGES;
```

- check privileges on certain user:

```
SHOW GRANTS FOR 'user'@'localhost';
```

- creating database:

```
CREATE DATABASE acme;
```

- to use the database:

```
USE acme;
```

- listing tables:

```
SHOW TABLES;
```

- creating tables:

```
CREATE TABLE users(
id INT AUTO_INCREMENT,
first_name VARCHAR(100),
last_name VARCHAR(100),
email VARCHAR(75),
password VARCHAR(255),
location VARCHAR(100),
dept VARCHAR(75),
is_admin TINYINT(1),
register_date DATETIME,
PRIMARY KEY(id)
);
```

- Showing tables will result now with a table
  named `users`.

- deleting database:

```
DROP DATABASE acme;
```

- listing all data from a table:

```
SELECT * FROM users;
```

- inserting record in MySQL tables:

```
INSERT INTO users(first_name, last_name, email,
password, location, dept, is_admin, register_date)
values ('John', 'Doe', 'john@gmail.com', '12345',
'Mssachusetts', 'development', 1, now());
```

- now again when you list the `users` table
  data you'll see the entry.

- adding multiple records:

```
use the command from cheatsheet
```

- selecting sepecific colunms from the database:

```
SELECT first_name, last_name FROM users;
```

- specifying the WHERE clause:

```
SELECT * FROM users WHERE location='Massachusetts' AND dept='sales';
```

- You can also use operators in the command:

```
SELECT * FROM users WHERE is_admin > 0;
```

- how to delete and update data in the database:

```
DELETE FROM users WHERE id = 6;
```

- updating data:

```
UPDATE users SET email = 'freddy@gmail.com'
WHERE id = 2;
```

- add a new column in a table:

```
ALTER TABLE users ADD age VARCHAR(3);
```

- modifying the columns in a table:

```
ALTER TABLE users MODIFY COLUMN age INT(3);
```

- order by stuffs:

```
SELECT * FROM users ORDER BY last_name DESC;
```

- concatening columns:

```
SELECT CONCAT(first_name, ' ', last_name) AS 'Name',
dept FROM users;
```

- one result with distinct location:

```
SELECT DISTINCT location FROM users;
```

- selecting ranges:

```
SELECT * FROM users WHERE age BETWEEN 20 and 30;
```

- full text searching for searching in a blogpost
  for example:

- any value that starts with 'd':

```
SELECT * FROM users WHERE dept LIKE 'd%';
```

- anything which starts with 'de'

```
SELECT * FROM users WHERE dept LIKE 'de%';
```

- anything which ends with 't':

```
SELECT * FROM users WHERE dept LIKE '%t';
```

- anything before and after 't':

```
SELECT * FROM users WHERE dept LIKE '%t%';
```

- anything which ends with 't':

```
SELECT * FROM users WHERE dept LIKE '%t';
```

- putting NOT LIKE will give the opposite results.

- using IN to use list:

```
SELECT * FROM users WHERE dept IN('design', 'sales');
```

- indexes in tables:

```
CREATE INDEX LIndex on users(location);
```

- removing index:

```
DROP INDEX LIndex on users;
```

- creating a table for a post:

```
CREATE TABLE posts(
id INT auto_increment,
user_id INT,
title VARCHAR(100),
body text,
publish_date DATETIME DEFAULT CURRENT_TIMESTAMP
PRIMARY KEY(id),
FOREIGN KEY(user_id) REFERENCES users(id)
);
```

- adding some data to the post table:

```
grabing it just from the cheatsheet
```

- The you can view the posts table data:

```
SELECT * FROM posts;
```

- joining tables

```
SELECT
users.first_name,
users.last_name,
posts.title,
posts.publish_date
FROM users
INNER JOIN posts
ON users.id = posts.user_id
ORDER BY posts.title;
```

- creating another table for comments:

```
CREATE TALE comments(
id INT AUTO_INCREMENT,
post_id INT,
user_id INT,
body TEXT,
publish_date DATETIME DEFAULT CURRENT_TIMESTAMP,
PRIMARY KEY(id),
FOREIGN KEY(post_id) REFERENCES posts(id),
FOREIGN KEY(user_id) REFERENCES users(id)
);
```

- inserting comments:

```
using the cheatsheet default data.
```

- and displaying the comment data by:

```
SELECT * FROM comments;
```

- selecting comments of the posts:

```
SELECT
comments.body;
posts.title;
FROM comments
LEFT JOIN posts ON posts.id = comment.post_id
ORDER BY posts.title
```

- from this you'll every comment that is connected
  to the posts.

- avoiding to display the posts which doesn't
  have any comments. (Use only LEFT JOIN for that!)

- now again pulling data with users details too:

```
SELECT
comment.body,
posts.title,
users.first_name,
users.last_name,
FROM comments
INNER JOIN posts ON posts.id = comments.post_id
INNER JOIN users ON users.id = comments.user_id
ORDER BY posts.title
```

- from this you'll get the data from posts,users,
  and comments table.

#### Aggregate Functions:

- using COUNT

```
SELECT COUNT(id) FROM posts;
```

- will return the count of all posts.

- using MAX:

```
SELECT MAX(age) FROM users;
```

- using MIN:

```
SELECT MIN(age) FROM users;
```

- using SUM:

```
SELECT SUM(age) FROM users;
```

- uppercase and lowercase:

```
SELECT UCASE(first_name), LCASE(last_name) FROM users;

```

- using GROUP BY:

```
SELECT location, COUNT(location) FROM users GROUP BY location;
```

- with the WHERE clause:

```
SELECT location, COUNT(location) FROM users WHERE location = 'Massachusetts' GROUP BY location;
```

### Creating a quick nodejs app:

- running `npm init -y` in new folder.

- create `index.js` file and write this code:

```
const express = require('express');
const mysql = require('mysql');

const app = express();

const db = mysql.createConnection({
    host: 'localhost',
    user: 'username',
    password: 'password',
    database: 'databasename'
});

db.connect();

app.get('/users', (req, res) => {
    const sql = 'SELECT * FROM users';

    db.query(sql, (err, result) => {
        if(err) throw err;
        res.send(result);
    });
});

app.listen(5000, () => console.log('Server started'));
```

- and run the code:
