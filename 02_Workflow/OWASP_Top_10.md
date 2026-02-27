# OWASP Top 10

## [A01 Broken Access Control](https://owasp.org/Top10/2025/A01_2025-Broken_Access_Control/) (IAAA)

### Description
Users are able to access information outside of their intended permissions.
Put differently: The server doesn't enfoce who can access what on every request.
An example could be IDOR.
Basically, the user input is not verified and instead blindly trusted.

#### IDOR
Example URL: `https://example.com/accounts?id=42`. If the ID isn't verified on each request, one can view data of other accounts

### What to do about it
- Enfore server-side checks on __every__ request

### How do find BAC vulnerabilities
- Capture relevant packages with BurpSuite
    - Registration
    - Login
- Look for redirects and sent parameters.
    - Send the packet to repeater and play round with the values
- Go to the netowrking tab in the browser and refresh the page
    - Look for calls to APIs with paramaeters given
    - Get the URL and manually modify the values

## A02 Security Misconfiguration

## A03 Software Supply Chain Failures

## A04 Cryptographic Failures

## A05 Injection

## A06 Insecure Design

## [A07 Authentication Failures](https://owasp.org/Top10/2025/A07_2025-Authentication_Failures/) (IAAA)

### Description
The server isn't able to properly verify the users identity. This leads to:
- username enumeration
- brute-forceable logins (because of missing lockout / rate limiting)
- logic flags in login or registration flow
- insecure session or cookie handling

### What to do about it
- Unique indexes (No duplicate usernames)
- Rate-limiting, lock out policy on brute-force
- Invalidate sessions on password or privilege changes

## A08 Software or Data Integrity Failures

## [A09 Security Logging and Alerting Failures](https://owasp.org/Top10/2025/A09_2025-Security_Logging_and_Alerting_Failures/) (IAAA)

### Description
If there are no alerts about possible attacks, defenders can't do their work. Accountability is important (logging).

### What to do about it
- Log full authentication lifecycle (fail/success, password/2FA, actions)
- Alert on anomalies (brute-force, PrivEsc)

## A10 Mishandling of Exceptional Conditions

## Further information

### IAAA
- Identification: The account that represents a person or service (ID, email)
- Authentication: Proving the identity (Password, OTP, Passkey)
- Authorisation: Privileges of the identity
- Accountability: Recording and alerting on who did what, when and from where.
