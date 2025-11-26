# What is Cross-Site Scripting (XSS)?

Cross-Site Scripting (XSS) is a client-side web vulnerability that allows an attacker to inject malicious JavaScript code into a web page viewed by other users.

When exploited successfully, XSS allows the attacker to:

- Steal cookies
- Steal localStorage/sessionStorage tokens
- Perform actions on behalf of a victim (CSRF-like)
- Deface websites
- Keylogging users
- Redirect users to malicious websites
- Bypass access controls

---

## Why does XSS happen?

XSS happens when **untrusted user input is processed and rendered without proper validation, encoding, or sanitization**.

