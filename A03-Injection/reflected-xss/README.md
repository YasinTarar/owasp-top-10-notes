# Reflected XSS in a search page

I entered a search term and checked where it appeared in the returned HTML. The page echoed it into the search results message, so I tried a small script in the same field.

```
<script>alert(1)</script>
```

An alert opened when I submitted the search. The input travelled in the request and came straight back in the response. A visitor opening a crafted search URL could run JavaScript in the context of that site.

For this HTML text context I would escape the search term when rendering it. A restrictive Content Security Policy gives the browser another way to block inline scripts.

## Screenshots

* [01 alert payload](screenshots/01-alert-payload.png)
* [02 popup result](screenshots/02-popup-result.png)

[Back to my PortSwigger injection labs](../README.md)
