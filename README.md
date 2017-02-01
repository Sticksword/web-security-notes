# web-security-notes
This is my user-friendly version of what I learned muddling around with web security stuff that I hope can be of use to you! :)

#### XSS:
* These attacks are a type of injection where malicious scripts are injected into normal websites that don't cleanse the data they output to the screen. In general to prevent XSS attacks, never accept JS code from an untrusted source and then run it.
* Examples:
 * Form input with value `<script>alert('XSS!');</script>` and then echoing this value upon form submit somewhere down the road
 * Query string input with value `example.php?id=%3Cscript%3Ealert%28%27XSS%21%27%29%3B%3C%2Fscript%3E` and then echoing this value on page load (similar to above)
 * These scripts can be non-persistent as demonstrated above or persisted. When fetching from a database, the values still have to be escaped since we store the actual values in the DB, not the escaped versions.
* Related threats: clickjacking (where HTML/JS is injected so that there is an invisible iframe or button on top of visible button) and cursorjacking (where cursor location is skewed by `x` pixels so that what you see isn't actually where cursor is)
* Solution: use `htmlspecialchars()` whenever outputting data from potentially untrusted sources
* See more:
 * http://stackoverflow.com/questions/4882307/when-to-use-htmlspecialchars-function
 
 
#### SQL Injection:
* These attacks are a type of injection where ''nefarious'' SQL statements are inserted into an entry field for execution.
* Examples:
 * Form input with value `sqli' OR (1=1 AND SLEEP(5)=0) --'` which then gets executed when inserting/updating the DB
 * Query string input with value `sqli%27+OR+%281%3D1+AND+SLEEP%285%29%3D0%29+--%27` (similar to above case)
* Solution: use `mysqli-real-escape-string()` for all data that comes in from the user
* See more:
 * http://stackoverflow.com/questions/11653059/when-to-use-mysqli-real-escape-string
 * http://stackoverflow.com/questions/60174/how-can-i-prevent-sql-injection-in-php
