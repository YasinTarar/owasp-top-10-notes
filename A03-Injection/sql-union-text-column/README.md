# Finding the column that accepts text

Once I had a three column result, I moved a test string between positions and checked the product page after each request.

```
' UNION SELECT NULL,'kBjBsW',NULL--
```

The page displayed my string when I put it in the middle position. That established two things about the second column. It accepted text and its value appeared in the response.

A database account with limited permissions reduces what a successful injection can read. The fix for the filter itself is a parameterised query.

## Screenshots

* [sqli union text column error](screenshots/sqli-union-text-column-error.png)
* [sqli union text column solved](screenshots/sqli-union-text-column-solved.png)
* [union attack lab homepage](screenshots/union-attack-lab-homepage.png)

[Back to my PortSwigger injection labs](../README.md)
