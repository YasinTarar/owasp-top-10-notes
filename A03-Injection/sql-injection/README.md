# SQL Injection — Retrieving Hidden Data

**Lab Source:** PortSwigger Web Security Academy  
**OWASP Category:** A03:2021 — Injection  
**Difficulty:** Apprentice

---

## What Is SQL Injection?

SQL Injection happens when an application includes untrusted user input directly inside a database query, without first checking or escaping it. This gives an attacker the ability to change what the query actually does.

The easiest way to picture it: the application is building a sentence to send to the database. If you can insert your own words into that sentence, you can completely change its meaning.

---

## The Lab Scenario

The target was a shopping application with a product category filter. When a user selected a category like "Gifts", the URL changed to:

```
/filter?category=Gifts
```

Behind the scenes, the application was running this SQL query:

```sql
SELECT * FROM products
WHERE category = 'Gifts'
AND released = 1
```

The `AND released = 1` condition was intentionally restricting the results — it was hiding unreleased products from regular users.

---

## Exploitation — Step by Step

**Step 1 — Identify the injection point**

The `category` parameter was being placed directly into the SQL query. If the application wasn't sanitising that input, I could change the query's logic by adding SQL syntax.

**Step 2 — Craft the payload**

I modified the URL to:

```
/filter?category=Gifts'+OR+1=1--
```

This changed the underlying query to:

```sql
SELECT * FROM products
WHERE category = 'Gifts'
OR 1=1--
AND released = 1
```

Breaking down what happened:
- `'` — closed the existing string that the category was wrapped in
- `OR 1=1` — added a condition that is always true, so every product matched
- `--` — commented out the rest of the query, including the `AND released = 1` restriction

**Step 3 — Result**

The application returned all products in the database, including the hidden unreleased ones.

---

## Screenshots

| Screenshot | Description |
|---|---|
| `01-login-page.png` | Initial state of the application |
| `02-hidden-data-before-injection.png` | Normal category filter — only released products visible |
| `03-admin-login-bypass.png` | After injection — hidden products now returned |

---

## Real-World Impact

In a real application, SQL injection can go much further than revealing hidden products. Depending on the database configuration and what the application does, an attacker could:

- Extract usernames, passwords, and personal data from any table
- Bypass login pages without knowing a valid password
- Modify or delete database records
- In some cases, read files from the server's filesystem or execute operating system commands

This is why SQL injection consistently features as one of the most serious web vulnerabilities.

---

## How to Prevent It

**Parameterised queries (the right fix)**

Instead of building a query by joining strings together:

```python
# Vulnerable
query = "SELECT * FROM products WHERE category = '" + category + "'"
```

Use a parameterised query that keeps the data separate from the SQL structure:

```python
# Safe
query = "SELECT * FROM products WHERE category = ?"
cursor.execute(query, (category,))
```

The database receives the category value as data, not as part of the query logic. Even if someone enters `' OR 1=1--`, it's treated as a literal string, not SQL.

**Additional defences**

- Use an ORM (like SQLAlchemy or Django ORM) which handles parameterisation automatically
- Validate and whitelist expected input types where possible
- Apply least-privilege database accounts — the web app shouldn't need `DROP TABLE` permissions
- Enable a Web Application Firewall (WAF) as an additional layer, not a replacement for fixing the root cause
