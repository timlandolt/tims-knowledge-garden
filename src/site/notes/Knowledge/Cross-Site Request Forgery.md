---
{"dg-publish":true,"permalink":"/knowledge/cross-site-request-forgery/","tags":["cyber-security","csrf"]}
---

---

> [!hint] aka. CSRF or Sea-Surf

=> Tricking the user's browser to call unwanted actions on a site

- Through crafted links that call get requests
- Through Sending POST requests (from other sites or through XSS)

## Solution
- Add anti-forgery token (in cookies or hidden form field)
- Only use GET requests RESTfully (only to show data)
- Require the user to re-authenticate before sensitive actions