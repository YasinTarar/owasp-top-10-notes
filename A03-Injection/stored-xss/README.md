# Stored XSS in blog comments

I submitted an ordinary comment first to see where it appeared. I then posted the same small script I used in the search lab.

```
<script>alert(1)</script>
```

The difference showed up when I reopened the post. The alert appeared again without submitting the form. The site had saved my comment and served it to the next page load, so a reader could trigger it simply by visiting the post.

I would render plain comments as escaped text. If the site needs formatting, I would sanitise the permitted HTML before rendering it.

## Screenshots

* [01 comment payload](screenshots/01-comment-payload.png)
* [02 popup alert](screenshots/02-popup-alert.png)
* [03 lab solved](screenshots/03-lab-solved.png)

[Back to my PortSwigger injection labs](../README.md)
