# PortSwigger Academy Notes

## SQL Injection

### What is SQL Injection (SQLi)

- SQL injection (SQLi) is a web securitu vulnerability that allows an attacker to interfere with
  the queries that an application makes to its database.

- This might include data that belongs to other users, or any other data that the application can
  access.

- In some situations, an attacker can escalate a SQL injection attack to compromise the underlying
  server or other back-end infrastructure. It can also enable them to perform denial-of-service
  attack.

### How to detect SQL injection vulnerabilies:

- You can detect SQL injection manually using a systematic set of tests agains every entry point
  in the application: - The single quote character `'` and look for errors or other anomalies. - Some SQL-specific syntax that evaluates to the base (original) value of the entry point, and
  to a different value, and look for systematic differences in the application responses. - Boolean conditions such as `OR 1=1` and `OR 1=2`, and look for differences in the application's
  responses.

### SQL injection in different parts of the query

- Most SQL injection vulnerabilities occur within the `WHERE` clause of a `SELECT` query. Most
  experienced testers are familiar with this type of SQL injection.

- However, SQL injection vulnerabilities can occur at any location within the query, and within
  different query types. Some other common locations where SQL injection arises are: - In `UPDATE` statements, within the updated values or the `WHERE` clause. - In `INSERT` statements, within the the inserted values. - In `SELECT` statements, within the table or column name. - In `SELECT` statements, within the `ORDER BY` clause.

### Retrieving hidden data

- Imagine a shopping application that displays products in different categories. When the user
  clicks on the `Gifts` category, their browser requests the URL:

```
https://insecure-website.com/products?category=Gifts
```

- This causes the application to make a SQL query to retrieve details of the relevant products from
  the database:

```
SELECT * FROM products WHERE category = 'Gifts' AND released = 1
```

- This SQL query asks the database to return:

  - all details (`*`)
  - from the `products` table
  - where the `category` is `Gifts`
  - and `released` is `1`.

- The restriction `released = 1` is being used to hide products that are not released. We could
  assume for unreleased products, `released  = 0`.

### Retrieving hidden data

- The application doesn't implement any defensed against SQL injection attacks. This means an
  attacker can construct the following attack, for example:

```
https://insecure-website.com/products?category=Gifts'--
```

- This results in the SQL query:

```
SELECT * FROM products WHERE category = 'Gifts'--' AND released = 1
```

- Crucially, note that `--` is a comment indicator in SQL. This means that the rest of the query is
  interpreted as a comment, effectively removing it.

- In this example, this means the query no longer include `AND released = 1`. As a result, all
  products are displayed, including those that are not yet released.

- You can use a similar attack to cause the application to display all the products in any category,
  including categories that they don't know about:

```
https://insecure-website.com/products?category=Gifts'+OR+1=1--
```

- This results in the SQL query:

```
SELECT * FROM products WHERE category = 'Gifts' OR 1=1--' AND released = 1
```

- The modified query returns all items where either the `category` is `Gifts`, or `1` is equal to
  `1`. As `1=1` is always true, the query returns all items.

> **Warning**: Take care when injecting the condition `OR 1=1` into a SQL query. Even if it appears
> to be harmless in the context you're injecting into, it's common for applications to use data from
> a single request in multiple different queries. If your condition reaches an `UPDATE` or `DELETE`
> statement, for example, it can result in an accidental loss of data.

### Lab: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data

- This lab contains a SQL injection vulnerability in the product category fiter. When the user
  selects a category, the application carries out a SQL query like the following:

```
SELECT * FROM products WHERE category = 'Gifts' AND released = 1
```

- To solve the lab, perform a SQL injection attack that causes the application to display one or
  more unreleased products. **LAB 01**: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data.
