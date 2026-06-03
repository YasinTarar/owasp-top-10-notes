# OWASP Top 10 — Web Security Learning Portfolio

This repository documents my hands-on practice with common web application vulnerabilities, using PortSwigger Web Security Academy labs as the primary learning environment.

Each lab write-up covers what the vulnerability is, how I exploited it in a controlled setting, what the real-world impact would be, and how developers can prevent it.

> **Context:** First year BSc Cybersecurity student at the University of Roehampton. This portfolio is a record of practical learning alongside my degree — not just theory, but actual exploitation and analysis.

---

## What's Covered

| OWASP Category | Vulnerability | Lab Source | Status |
|---|---|---|---|
| A03 — Injection | SQL Injection | PortSwigger | ✅ Complete |
| A03 — Injection | Reflected XSS | PortSwigger | ✅ Complete |
| A03 — Injection | Stored XSS | PortSwigger | ✅ Complete |
| A03 — Injection | DOM-Based XSS | PortSwigger | ✅ Complete |
| A03 — Injection | SQL UNION Column Count | PortSwigger | ✅ Complete |
| A03 — Injection | SQL UNION Text Column | PortSwigger | ✅ Complete |

More categories being added as I work through them.

---

## Tools Used

- **PortSwigger Web Security Academy** — lab environment
- **Burp Suite Community Edition** — request interception and analysis
- **Browser DevTools** — DOM inspection and source analysis

---

## Repository Structure

```
owasp-top-10-notes/
└── A03-Injection/
    ├── sql-injection/
    │   ├── README.md
    │   └── screenshots/
    ├── sql-union-column-count/
    │   ├── README.md
    │   └── screenshots/
    ├── sql-union-text-column/
    │   ├── README.md
    │   └── screenshots/
    ├── reflected-xss/
    │   ├── README.md
    │   └── screenshots/
    ├── stored-xss/
    │   ├── README.md
    │   └── screenshots/
    └── dom-xss/
        ├── README.md
        └── screenshots/
```

---

## How to Read These Write-Ups

Each lab folder follows the same structure:

1. **What the vulnerability is** — plain-English explanation
2. **The lab scenario** — what the target application looked like
3. **How I exploited it** — step by step, with screenshots
4. **Real-world impact** — what this would mean outside a lab
5. **How to prevent it** — the developer's perspective

---

## About Me

BSc Cybersecurity student, University of Roehampton (Year 1 — First Class result).  
Interested in web application security, penetration testing, and threat analysis.

[GitHub Profile →](https://github.com/YasinTarar)
