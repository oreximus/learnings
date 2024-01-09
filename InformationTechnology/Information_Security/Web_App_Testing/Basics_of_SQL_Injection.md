# Notes on "Basics of SQL Injection"

### Source: https://www.youtube.com/watch?v=2nXOxLpeu80

## Testing Stuffs

1. SBVA, a already Configured Vulnerable PHP Web Application to Test.
2. testphp, a vulnerable web-application for Testing Purposes by acunetix.

## Classic SQL Injection

- Using the Commenting Technique to Bypass the Login Check:

```
\\ In Username Section

' OR 1=1 -- -

\\ Type any password in the password section
\\ Or you can leave it blank!
```

- There are various to way to comment out things in the SQL query try
  experimenting with different ones too.

## Types of SQL Injection

### Two Major Categories of SQL Injection:

1. In-band SQL Injections
2. Infrential SQL Injections

### One very rare Case of SQL Injections, Third Category:

3. Out of Band SQL Injection
   - Not applicable in many of SQL products,
   - majorly found in the databases of Oracle under a special package called:
     UTL_HTTP, with which we can a response in our netcat listener, and there we
     can response of our queries.
   - They do not lie in the application itself, rather they occur in the
     background like can occur in the netcat listener which could be setted-up
     by us.

### 1. In-band SQL Injections

- They usually occurs when you get some kind of response from the website,
  either you get some kind of **data** in response or it could be an **error**.

**In Case of Data**:

- We can manipulate the Data through SQL injections, and that's why they also
  known as `Data-Based SQL Injections`!
- In `Data-Based SQL Injections`, we can use the Technique called: **Union Based
  SQL Injection**. Where we will use the UNION command of SQL.
- When we get the Data from the application we probably go with the **Union
  Based SQL Injection** technique.

**In Case of Error**:

- When we can take the Advantage of Error to inject our SQL, that's when we use
  **Error based SQL Injection** technique.

#### Union based SQL injections:

- Union based sql injections occurs when we are able to use the UNION operator
  to combine the output of two select Statements.

### 2. Infrential SQL Injections

- In some cases we do not get any Data or any Error, then there we need to
  analyze the Behaviour of application.

**Two Techniques of `Infrential SQL Injections`:

1. Boolean-Based SQL Injection (True/False)
2. Time-Based SQL Injection (Time taken by the application)

## Todo

- Learn the Basics of SQL, for Basic Operation.
