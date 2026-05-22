# owasp-top-10-notes
Notes and practical examples of common web security vulnerabilities.

## SQL Injection

SQL Injection is a web security vulnerability where an attacker is able to inject SQL code into an application’s database query.

The simplest way to understand it is that the website trusts user input too much. If the input is placed directly into a SQL query without proper protection, the attacker can change the logic of the query.

For example, a normal query may check if a username and password are correct:

```sql
SELECT * FROM users 
WHERE username='yasin' 
AND password='123';

If an attacker enters:

' OR 1=1--

the query can be changed so that the condition becomes always true. The 1=1 part is always true and the -- comments out the rest of the query, which can stop the password check from being used.

In the PortSwigger lab, I tested SQL injection in a product category filter. The normal page only showed released products, but by changing the URL parameter to include:

Gifts' OR 1=1--

the application displayed additional hidden products.

What I learned

SQL injection works by changing the structure of a database query through user input. It can be used to retrieve hidden data, bypass logins, or access information from other database tables.

Impact

A successful SQL injection attack could lead to sensitive data being exposed, accounts being accessed without permission, or database information being modified.

Prevention

SQL injection can be prevented by using parameterised queries, prepared statements, input validation, and least privilege database permissions.
