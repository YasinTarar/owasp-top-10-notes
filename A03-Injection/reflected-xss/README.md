# Reflected Cross-Site Scripting (XSS)

**Lab Source:** PortSwigger Web Security Academy  
**OWASP Category:** A03:2021 — Injection  
**Difficulty:** Apprentice

---

## What Is Reflected XSS?

Reflected XSS happens when an application takes user input, includes it in the HTTP response without sanitising it, and the browser executes it as code rather than displaying it as text.

The word "reflected" describes the flow: the payload goes in, hits the server, and bounces straight back out inside the page. It's not stored anywhere — it only fires for the person who sends the malicious request, which is why it usually requires a victim to click a crafted link.

---

## The Lab Scenario

The target application had a search bar. When a user searched for something, the search term was reflected back into the page in a message like:

```
You searched for: boots
```

The search term was being placed directly into the HTML without any encoding or filtering.

---

## Exploitation — Step by Step

**Step 1 — Confirm the reflection**

I entered a basic test string in the search bar and checked the page source to see exactly where and how it appeared in the HTML.

**Step 2 — Test for script execution**

I submitted:

```html
<script>alert(1)</script>
```

**Step 3 — Result**

The application reflected the input directly into the page without escaping it. The browser parsed the `<script>` tags as HTML and executed the JavaScript, causing an alert box to pop up displaying `1`.

This confirmed that the application was treating user input as trusted HTML rather than plain text.

---

## Screenshots

| Screenshot | Description |
|---|---|
| `01-alert-payload.png` | Payload entered into the search bar |
| `02-popup-result.png` | Alert box triggered in the browser |

---

## Real-World Impact

`alert(1)` is just a proof of concept — it demonstrates the vulnerability exists, but the actual damage in a real attack would be much more significant.

With reflected XSS, an attacker could:

- Steal a victim's session cookie by redirecting it to an attacker-controlled server
- Capture keystrokes or form submissions (credentials, payment details)
- Redirect the victim to a phishing page
- Modify the content of the page to display false information
- Perform actions on the victim's behalf if they're logged in

The attack typically requires the victim to click a specially crafted link containing the payload in the URL. These links are often distributed through phishing emails or messages.

---

## How to Prevent It

**Output encoding**

When user input is included in an HTML page, it needs to be encoded so the browser treats it as text rather than HTML or JavaScript. Most templating engines do this automatically.

For example, `<script>alert(1)</script>` should be rendered as:

```
&lt;script&gt;alert(1)&lt;/script&gt;
```

The browser displays those characters as literal text rather than executing them as code.

**Content Security Policy (CSP)**

CSP is an HTTP header that tells the browser which sources of scripts are allowed to run. A strict policy can prevent inline scripts like `<script>alert(1)</script>` from executing entirely, even if they're reflected into the page.

**Input validation**

Validate input on the server side. If a field expects a search term, it shouldn't accept angle brackets or script tags. Validation alone isn't sufficient — it needs to work alongside output encoding — but it reduces the attack surface.

**Framework defaults**

Modern frameworks like React, Angular, and Django's templating engine automatically escape output by default. Avoid bypassing these defaults unless absolutely necessary.
