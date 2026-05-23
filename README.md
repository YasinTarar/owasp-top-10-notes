# owasp-top-10-notes

Notes and practical examples of common web security vulnerabilities.

## SQL Injection

SQL Injection is a web security vulnerability where an attacker is able to inject SQL code into a website’s database query.

The simplest way to understand SQL injection is that the website trusts user input too much. If user input is placed directly into a SQL query without proper protection, an attacker can change how the query works.

For example, a normal login query may look like this:

```sql
SELECT * FROM users 
WHERE username='yasin' 
AND password='123';
```

If an attacker enters:

```sql
' OR 1=1--
```

the query logic changes. The `1=1` condition is always true and the `--` comments out the rest of the query, which can remove the password check.

In the PortSwigger lab, I tested SQL injection in a product category filter. The normal page only displayed released products, but by changing the URL parameter to:

```sql
Gifts' OR 1=1--
```

the application displayed additional hidden products.

### What I learned

SQL injection works by changing the structure of a database query through user input. It can be used to retrieve hidden data, bypass logins, or access information from other database tables.

### Impact

A successful SQL injection attack could lead to sensitive information being exposed, accounts being accessed without permission, or database information being modified.

### Prevention

SQL injection can be prevented by using parameterised queries, prepared statements, input validation, and least privilege database permissions.

---

## Reflected Cross Site Scripting (XSS)

Reflected XSS is a web vulnerability where user input is displayed back onto a webpage without proper filtering or encoding.

In this lab, the website had a search bar that reflected the search input directly into the page. By entering:

```html
<script>alert(1)</script>
```

the browser treated the input as JavaScript code instead of plain text and executed it.

This caused a popup box to appear showing:

```text
1
```

### What I learned

Reflected XSS works when a website trusts user input too much and sends it back into the webpage without sanitising it correctly. The browser then executes the injected JavaScript.

### Impact

A successful XSS attack could allow an attacker to steal session cookies, capture user input, redirect users, or modify webpage content.

### Prevention

XSS can be prevented by properly encoding output, sanitising user input, using secure frameworks, and implementing Content Security Policy (CSP).
