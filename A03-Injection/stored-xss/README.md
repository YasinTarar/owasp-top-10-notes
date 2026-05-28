# Stored Cross-Site Scripting (XSS)

**Lab Source:** PortSwigger Web Security Academy  
**OWASP Category:** A03:2021 — Injection  
**Difficulty:** Apprentice

---

## What Is Stored XSS?

Stored XSS (also called persistent XSS) is a variant of cross-site scripting where the malicious payload is saved on the server — usually in a database — and then served to other users when they visit the affected page.

This makes it significantly more dangerous than reflected XSS. The attacker doesn't need a victim to click a crafted link. Anyone who visits the page receives and executes the payload automatically.

---

## The Lab Scenario

The target application had a blog with a comment section. Users could submit comments, which were then stored and displayed to anyone viewing the post.

The application was not sanitising or encoding comment content before saving or displaying it. This meant any HTML or JavaScript submitted in a comment would be rendered as actual code in the browser.

---

## Exploitation — Step by Step

**Step 1 — Identify the stored input point**

The comment field accepted free-text input that was then displayed on the page. I checked the page source after submitting a basic comment to confirm the text was being placed directly into the HTML without any encoding.

**Step 2 — Inject the payload**

I submitted a comment containing:

```html
<script>alert(1)</script>
```

**Step 3 — Payload stored**

The application accepted and saved the comment without any validation or sanitisation.

**Step 4 — Result**

Every time any user loaded the blog post page, the browser retrieved the stored comment from the server and executed the embedded JavaScript. An alert box appeared for every visitor, confirming persistent code execution.

---

## Screenshots

| Screenshot | Description |
|---|---|
| `01-comment-payload.png` | Payload submitted in the comment field |
| `02-popup-alert.png` | Alert box triggered on page load |
| `03-lab-solved.png` | Lab completion confirmation |

---

## Real-World Impact

Because the payload fires for every user who visits the page, stored XSS can have a much wider blast radius than reflected XSS.

In a real application, an attacker could use stored XSS to:

- **Mass steal session cookies** — every logged-in user who visits the page has their session token sent to the attacker
- **Perform actions on behalf of victims** — submit forms, change account settings, make purchases
- **Spread malware** — redirect visitors to exploit kits or malicious downloads
- **Deface the page** — replace legitimate content with attacker-controlled content
- **Capture credentials** — replace login forms with fake versions

If the affected page is something like an admin dashboard, a single stored XSS payload could compromise privileged accounts.

---

## How to Prevent It

**Output encoding**

Every piece of user-generated content must be encoded before being inserted into HTML. The browser then renders it as text rather than parsing it as code.

```html
<!-- What should be stored and rendered: -->
&lt;script&gt;alert(1)&lt;/script&gt;

<!-- What the user sees: -->
<script>alert(1)</script>
```

**Input validation and sanitisation**

Validate input at the point of submission. For comment fields, there's rarely a legitimate reason to accept raw HTML — strip or reject tags that aren't explicitly allowed.

If rich text input is required (bold, links, etc.), use a sanitisation library like DOMPurify rather than trying to write your own filter. Custom filters are very easy to bypass.

**Content Security Policy (CSP)**

A well-configured CSP header restricts which scripts the browser is allowed to execute. Even if a payload is stored and returned in the page, a strict CSP can prevent the browser from running it.

**Frameworks**

Templating engines in frameworks like Django, Rails, and React escape output by default. Avoid using raw HTML rendering (`dangerouslySetInnerHTML` in React, for example) unless the content has been explicitly sanitised first.
