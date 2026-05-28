# SQL Injection UNION attack determining the number of columns returned by the query

## Overview

This lab focused on using a UNION based SQL injection attack to determine the number of columns returned by the original database query.

The vulnerability existed within the product category filter parameter. By injecting UNION SELECT statements into the URL, it was possible to observe how the backend database handled different column counts.

## Objective

The objective of the lab was to identify the correct number of columns required for a successful UNION based SQL injection attack.

## Method

Different payloads containing NULL values were tested within the category parameter.

The first attempts caused Internal Server Error responses because the number of supplied columns did not match the original query structure.

The following payload successfully solved the lab:

```sql
' UNION SELECT NULL,NULL,NULL--
```

This confirmed that the original query returned three columns.

## Key Learning Points

* UNION based SQL injection requires the same number of columns as the original query
* NULL values are commonly used because they are compatible with most database column types
* Error responses can reveal information about backend database behaviour
* SQL injection vulnerabilities can expose sensitive application logic if user input is not handled securely

## Tools Used

* Burp Suite Community Edition
* Google Chrome
* PortSwigger Web Security Academy

## Screenshots

Screenshots showing the injection attempts and successful payload are included in the screenshots folder.
