# Retrieving hidden products

I changed the product category filter to see whether the database would still enforce the restriction on unreleased products.

```
/filter?category=Gifts'+OR+1=1--
```

The quote closed the category string. The condition `OR 1=1` matched every row and the SQL comment removed the release check from the rest of the statement. The page returned products that the original filter hid.

I would bind the category as a parameter. The database can then use it as a value without letting it change the query. Restricting the application account’s permissions also limits what an attacker could access.

## Screenshots

* [01 login page](screenshots/01-login-page.png)
* [02 hidden data before injection](screenshots/02-hidden-data-before-injection.png)
* [03 admin login bypass](screenshots/03-admin-login-bypass.png)

[Back to my PortSwigger injection labs](../README.md)
