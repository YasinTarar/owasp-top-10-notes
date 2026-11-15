# DOM XSS in a tracking image

I used browser DevTools to follow a search value from the URL into a tracking image. The page built the image markup with `document.write()` and placed the value inside a quoted attribute.

```
"><svg onload=alert(1)>
```

The opening quote in my input closed the attribute. The next character closed the image tag, allowing the browser to parse an SVG element and run its load handler. The vulnerable step happened in the page’s JavaScript.

I would create the image with DOM methods, use a fixed image path and set its query parameter with URLSearchParams. For displaying a search term as plain text, I would use `textContent`.

## Screenshots

* [01 inspect vulnerable code](screenshots/01-inspect-vulnerable-code.png)
* [02 payload in url](screenshots/02-payload-in-url.png)

[Back to my PortSwigger injection labs](../README.md)
