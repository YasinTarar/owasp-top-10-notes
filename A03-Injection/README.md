# A03:2021 — Injection

Injection vulnerabilities occur when untrusted data is sent to an interpreter as part of a command or query. The interpreter executes the data as code rather than treating it as plain text, which gives an attacker the ability to change the intended behaviour of the application.

In the OWASP Top 10 (2021 edition), Injection moved to the third position. It covers a broad family of attacks — SQL injection, cross-site scripting, command injection, and more.

---

## Labs Completed

| Vulnerability | Description | Folder |
|---|---|---|
| SQL Injection | Manipulating database queries via unsanitised user input | [sql-injection/](./sql-injection/) |
| Reflected XSS | Injecting scripts that are reflected back in the HTTP response | [reflected-xss/](./reflected-xss/) |
| Stored XSS | Injecting persistent scripts that execute for every user who visits a page | [stored-xss/](./stored-xss/) |
| DOM-Based XSS | Client-side script injection through unsafe DOM manipulation | [dom-xss/](./dom-xss/) |

---

## Why Injection Matters

Injection attacks have been a top vulnerability for over a decade. They're common because:

- Developers often trust user input without validating or sanitising it
- Legacy codebases frequently use string concatenation to build queries
- Input can reach an interpreter through many routes — URL parameters, form fields, headers, cookies

A single injection vulnerability in the right place can compromise an entire application or its underlying database.

---

## Common Prevention Principles

While each vulnerability type has its own specific fix, the underlying defence is consistent:

- **Never trust user input** — always validate and sanitise
- **Use parameterised queries** — separate data from code
- **Encode output** — make injected content harmless when rendered
- **Apply the principle of least privilege** — limit what an exploited component can actually do
