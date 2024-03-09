# Reflected XSS

## Source: https://book.hacktricks.xyz/pentesting-web/xss-cross-site-scripting

## What to Look For?

- You need to find **a value controlled by you that is being reflected** in the webpage.

    - **Intermediately Reflected**: If you find that the value of parameter or even the path is being reflected in the web page you could exploit a **Reflected XSS**.
    - **Stored and Reflected**: If you find that a value controlled by you is saved in the server and is reflected every time you access a page you could exploit a **Stored XSS**.
    - **Accessed via JS**: If you find that a value controlled by you is being access using JS you could exploit a **DOM XSS**.

## Context

- When trying to exploit a XSS the first thing you need to know is **where is your input being reflected**. Depending on the context, you will be able to execute arbitrary JS code on different ways.

## Raw HTML

- If your input is **reflected on the raw HTML** page you will need to abuse some **HTML tag** in order to execute JS code: `<img , <iframe , <svg , <script ` ... these are just some of the many possible HTML tags you could use.

- Also, keep in mind **Client Side Template Injection**.

## Inside HTML tags attributes


