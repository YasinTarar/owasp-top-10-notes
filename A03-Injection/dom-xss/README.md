# DOM-Based Cross-Site Scripting (XSS)

**Lab Source:** PortSwigger Web Security Academy  
**OWASP Category:** A03:2021 — Injection  
**Difficulty:** Apprentice

---

## What Is DOM-Based XSS?

DOM-based XSS is the most misunderstood of the three XSS types because the attack happens entirely inside the browser — the server never sees the payload at all.

In reflected and stored XSS, the vulnerability is in the server's response. In DOM XSS, the vulnerability is in client-side JavaScript that reads from a user-controllable source (like the URL) and writes it into the page in an unsafe way.

Two key concepts make this easier to understand:

- **Source** — where the attacker-controlled data enters the JavaScript (e.g. `location.hash`, `location.search`, `document.referrer`)
- **Sink** — the dangerous function that takes that data and writes it into the DOM (e.g. `document.write()`, `innerHTML`, `eval()`)

If there's a path from a source to a sink without proper sanitisation in between, there's a DOM XSS vulnerability.

---

## The Lab Scenario

The target application had a search feature. The page used JavaScript to read the search query from the URL and display it back to the user using `document.write()`.

Looking at the page source, the relevant code looked something like this:

```javascript
var search = document.getElementById('searchMessage');
document.write('<img src="/resources/images/tracker.gif?searchTerms=' + location.search + '">');
```

The URL parameter was being taken directly from `location.search` and written into the DOM via `document.write()`. No encoding, no sanitisation.

---

## Exploitation — Step by Step

**Step 1 — Inspect the source**

I opened DevTools and searched for where the URL parameter appeared in the page source. I could see it being inserted directly inside an `<img>` tag attribute via `document.write()`.

**Step 2 — Understand the context**

The payload was landing inside an HTML attribute value (the `src` of an `<img>` tag). To inject executable JavaScript, I needed to break out of that attribute first.

**Step 3 — Craft the payload**

I modified the URL search parameter to:

```
"><svg onload=alert(1)>
```

Breaking this down:
- `"` — closed the existing `src` attribute value
- `>` — closed the `<img>` tag entirely
- `<svg onload=alert(1)>` — injected a new SVG element with an `onload` event handler

**Step 4 — Result**

When the page loaded, the JavaScript wrote my payload into the DOM. The browser parsed the SVG element, and the `onload` event fired automatically, executing `alert(1)`.

---

## Screenshots

| Screenshot | Description |
|---|---|
| `01-inspect-vulnerable-code.png` | DevTools showing the unsafe `document.write()` call |
| `02-payload-in-url.png` | Payload injected via the URL search parameter |

---

## What Makes DOM XSS Harder to Detect

Because the payload never hits the server, traditional server-side security controls (input validation at the application layer, WAF rules checking request bodies) often won't catch it. The malicious string exists only in the URL fragment or other client-side data sources.

This also means server-side logs may show no obvious sign of an attack.

---

## Real-World Impact

The impact of DOM XSS is the same as other XSS types once execution is achieved:

- Session hijacking via cookie theft
- Credential harvesting
- Redirection to malicious sites
- Performing actions on behalf of the victim
- Modifying page content

DOM XSS is particularly common in single-page applications (SPAs) where JavaScript handles routing and rendering, and developers are more likely to manipulate the DOM directly.

---

## How to Prevent It

**Avoid dangerous sinks**

The most direct fix is to avoid functions that write raw HTML into the page. `document.write()`, `innerHTML`, and `outerHTML` are the most common culprits.

Use safe alternatives instead:

```javascript
// Dangerous
document.write('<p>' + userInput + '</p>');
element.innerHTML = userInput;

// Safe
element.textContent = userInput;  // treats input as text, not HTML
```

**Sanitise before inserting**

If you genuinely need to insert HTML (e.g. rich text content), use a trusted sanitisation library like DOMPurify before passing anything to a sink:

```javascript
element.innerHTML = DOMPurify.sanitize(userInput);
```

**Encode URL parameters**

If you're reading data from the URL to display on the page, encode it properly using `encodeURIComponent()` or an equivalent before inserting it into the DOM.

**Content Security Policy (CSP)**

A strict CSP can block inline event handlers like `onload=alert(1)`, significantly raising the bar for exploitation even when a DOM XSS sink exists.

**Code review and static analysis**

DOM XSS vulnerabilities are best caught during code review. Tools like Semgrep and ESLint with security plugins can flag dangerous sink usage automatically during development.
