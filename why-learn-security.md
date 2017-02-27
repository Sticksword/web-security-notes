# Whollistic viewpoint of security in my own words
This way, you're not thinking "why am I doing this" and more so "ohh so this is how it fits into the bigger picture". It's also to peak your interest and show you what is possible.

## __Application Security__

## Input Validation
When you build an application, you want to check for valid input to prevent malicious 

### Possible attacks
* Buffer overflow
* Cross-site scripting
* SQL injection
* canonicalization

## Software Tampering
When you build an application, there is always source code and that can sometimes be manipulated.
### Possible attacks
* Attacker modifies an existing application's runtime behavior to perform unauthorized actions
* Exploited via binary patching, code substitution, or code extension
blah

## Authentication
When you build an application, you have to be able to identify and verify the person is the actual person.
### Possible attacks
* Network eavesdropping
* Brute force attack
* Dictionary attacks
* Cookie replay
* Credential theft

### Authorization
When you build an application, you have to be able to identify what a person is allowed to do and what they have access to.
### Possible attacks
* Elevation of privilege
* Disclosure of confidential data
* Data tampering
* Luring attacks

## Configuration management
When you build an application, you have to make sure to add a layer of authentication and authorization for admin GUI's.
### Possible attacks
* Unauthorized access to administration interfaces
* unauthorized access to configuration stores
* retrieval of clear text configuration data; lack of individual accountability
* over-privileged process and service accounts

## Sensitive information
When you build an application, make sure any sensitive information is protected accordingly using encryption, salts, and whatnot.
### Possible attacks
* Access sensitive code or data in storage
* Network eavesdropping
* Code/data tampering

## Session management
When you build an application, make sure you aren't allowing people to steal authentication/authorization.
### Possible attacks
* Session hijacking
* Session replay
* Man in the middle

## Cryptography
When you build an application, make sure to use proper methods to encrypt and secure sensitive information.
### Possible attacks
* Poor key generation or key management
* Weak or custom encryption

## Parameter manipulation
When you build an application, often times you'll have to accept parameters for HTTP requests and we want to filter out bad/malicious requests.
### Possible attacks
* Query string manipulation
* Form field manipulation
* Cookie manipulation
* HTTP header manipulation

## Exception management
When you build an application, make sure when things go wrong, you don't tell the user anything relevant about the underlying system.
### Possible attacks
* Information disclosure
* Senial of service

## __OTHER__

## Malware download and phishing
When you visit websites, often times there will be attempts to run
### Possible attacks
* Software gets downloaded and user accidentally runs it
* Software installs a Chrome extension and user accidentally accepts it
* Email sent out pretending to be from authorized source and you provide authentication credentials

