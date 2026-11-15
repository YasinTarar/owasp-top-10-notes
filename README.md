# My web security labs

I worked through six PortSwigger Web Security Academy labs to understand how a search term, a comment or a product filter can change what an application does. I used Burp Suite Community Edition to inspect requests and browser DevTools to follow values into the page.

## SQL injection and XSS

1. [Retrieving hidden products](A03-Injection/sql-injection/README.md)
2. [Counting columns with SQL UNION](A03-Injection/sql-union-column-count/README.md)
3. [Finding the column that accepts text](A03-Injection/sql-union-text-column/README.md)
4. [Reflected XSS in a search page](A03-Injection/reflected-xss/README.md)
5. [Stored XSS in blog comments](A03-Injection/stored-xss/README.md)
6. [DOM XSS in a tracking image](A03-Injection/dom-xss/README.md)

The two UNION labs build on each other. First I used NULL values to work out how many columns the query returned. Then I moved a string between those columns until I could see it on the page. In the XSS labs the most useful question was whether the input came back immediately, persisted for the next visitor or became executable when the browser built the page.

I study Cyber Security at the University of Roehampton. My [home lab](https://github.com/YasinTarar/cyber-security-home-lab) covers the Linux and network side of my work.
