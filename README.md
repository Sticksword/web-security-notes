# web-security-notes
This is my user-friendly version of what I learned muddling around with web security stuff that I hope can be of use to you. Feel free to contribute! Simply fork and make a pull request :)

__Special thanks to CodePath for letting me take their Web Security course and learning all of this!!__

### XSS:
* These attacks are a type of injection where malicious scripts are injected into normal websites that don't cleanse the data they output to the screen. In general to prevent XSS attacks, never accept JS code from an untrusted source and then run it.
* __Examples__:
 * Form input with value `<script>alert('XSS!');</script>` and then echoing this value upon form submit somewhere down the road
 * Query string input with value `example.php?id=%3Cscript%3Ealert%28%27XSS%21%27%29%3B%3C%2Fscript%3E` and then echoing this value on page load (similar to above)
 * These scripts can be non-persistent as demonstrated above or persisted. When fetching from a database, the values still have to be escaped since we store the actual values in the DB, not the escaped versions.
* __Related threats__: clickjacking (where HTML/JS is injected so that there is an invisible iframe or button on top of visible button), cursorjacking (where cursor location is skewed by `x` pixels so that what you see isn't actually where cursor is), cookie theft/manipulation (sending browser cookie info elsewhere)
* __Solution__: use `htmlspecialchars()` whenever outputting data from potentially untrusted sources
* __See more__:
 * http://stackoverflow.com/questions/4882307/when-to-use-htmlspecialchars-function
 
### SQL Injection:
* These attacks are a type of injection where ''nefarious'' SQL statements are inserted into an entry field for execution.
* __Examples__:
 * Form input with value `sqli' OR (1=1 AND SLEEP(5)=0) --'` which then gets executed when inserting/updating the DB
 * Query string input with value `sqli%27+OR+%281%3D1+AND+SLEEP%285%29%3D0%29+--%27` (similar to above case)
* __Solution__: use `mysqli-real-escape-string()` for all data that comes in from the user
* __See more__:
 * http://stackoverflow.com/questions/11653059/when-to-use-mysqli-real-escape-string
 * http://stackoverflow.com/questions/60174/how-can-i-prevent-sql-injection-in-php

### Cross Site Request Forgery (CSRF attacks):
* A hacker site that is not same domain as an important site like `Citi.com` can mimic a request by forcing a user to make a GET or POST request upon loading of the hacker site. This in combination with the browser's stored authentication can lead to problems since the request will then be authenticated and potentially carried through.
* __Examples__:
 * onload of `hacker-way.com`, the site can submit a form that mimics the Citi form for making a transaction
 * a CSRF get request can be hidden away in an image src link so that upon load, the GET request for the "image" is made
 * basically onload of a site, bad things can happen if there is authentication information stored in a browser unless protected against
* __Solution__: First of all ensure same domains. One problem, the source domain can spoofed by the attacker. In that case, make GET requests harmless (only retrieval of non-sensitive information) and stick a CSRF token into all forms (eg. hidden <input> csrf token in post param) so that POST requests can be validated upon receipt.
 
### Session hijacking:
* Session ID's are sent per request and are also stored in cookies. If found out, an attacker can use the info to mascarade as the real user. No bueno.
* __Examples__:
 * From an XSS attack, a cookie's info can be stolen and from it, a session ID can be retrieved for ill use.
 * If the connection is not over HTTPS, an attacker can listen in on the request and get the session ID.
* __Solution__: Store session ID's in HttpOnly cookies (prevents attacker from finding out session ID in a cookie through XSS attack), only do HTTPS connections, refresh sessions every so often
 
### Session fixation:
* Kind of like opposite of session hijacking, it's when you provide the user with a session ID to use so that they authenticate through that session ID. After authenticating, the attacker now has an authenticated session ID to use for ill means.
* How can a session ID be "given" or set? You can alter responses via Man in the Middle attacks, affix a session ID to any url of a website so that the browser then uses that as the session ID, set it via XSS, 
* __Solution__: Use HttpOnly cookies to prevent XSS session fixation (JS cannot access HttpOnly cookies), don't accept session ID's as GET or POST params, and most importantly, refresh session identifiers after login (erases all previous fixations)(use `session_regenerate_id()`)
* __See more__:
 * http://stackoverflow.com/questions/22965067/when-and-why-i-should-use-session-regenerate-id

### Sample attack markup format:
* description
* __Examples__:
 * example 1
 * example 2
* __Solution__: what method to use to combat this
* __See more__:
 * link 1
