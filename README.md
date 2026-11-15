# My OWASP Top 10 web security portfolio

I use PortSwigger Web Security Academy to practise finding and testing vulnerabilities in web applications.

Each lab write-up covers what the vulnerability is, how I exploited it in a controlled setting, what the real-world impact would be, and how developers can prevent it.

> I started these labs alongside my Cyber Security degree at the University of Roehampton.

## What's Covered

| OWASP Category | Vulnerability | Lab Source | Status |
|---|---|---|---|
| A03 Injection | SQL Injection | PortSwigger | ✅ Complete |
| A03 Injection | Reflected XSS | PortSwigger | ✅ Complete |
| A03 Injection | Stored XSS | PortSwigger | ✅ Complete |
| A03 Injection | DOM-Based XSS | PortSwigger | ✅ Complete |
| A03 Injection | SQL UNION Column Count | PortSwigger | ✅ Complete |
| A03 Injection | SQL UNION Text Column | PortSwigger | ✅ Complete |

More categories being added as I work through them.

## Tools Used

* **PortSwigger Web Security Academy.** Lab environment
* **Burp Suite Community Edition.** Request interception and analysis
* **Browser DevTools**, DOM inspection and source analysis

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

## How to Read These Write-Ups

Each lab folder follows the same structure:

1. **What the vulnerability is.** Plain-English explanation
2. **The lab scenario.** What the target application looked like
3. **How I exploited it.** Step by step, with screenshots
4. **Real-world impact.** What this would mean outside a lab
5. **How to prevent it.** The developer's perspective

## About Me

BSc Cybersecurity student, University of Roehampton (First Class result in Year 1).  
Interested in web application security, penetration testing, and threat analysis.

[GitHub Profile →](https://github.com/YasinTarar)
