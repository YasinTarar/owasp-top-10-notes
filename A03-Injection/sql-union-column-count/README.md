# Counting columns with SQL UNION

I tried adding a second result to the category query. I started with one NULL, then two. Both attempts produced a server error.

```
' UNION SELECT NULL,NULL,NULL--
```

Three NULL values worked. That told me the original query returned three columns. NULL was useful here because I could test the shape of the result before finding out which column accepted text.

I would parameterise the category query. Hiding detailed database errors can reduce the information exposed, but the query still needs fixing.

## Screenshots

* [01 normal category page](screenshots/01-normal-category-page.png)
* [02 one column error](screenshots/02-one-column-error.png)
* [03 two column error](screenshots/03-two-column-error.png)
* [04 three column success](screenshots/04-three-column-success.png)

[Back to my PortSwigger injection labs](../README.md)
