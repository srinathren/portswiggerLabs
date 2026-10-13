# PortSwigger Web Security Academy: Insecure Direct Object References (IDOR)

## Lab Description
This lab contains an Insecure Direct Object Reference (IDOR) vulnerability in its user account functionality. An attacker can exploit this flaw to view or manipulate sensitive user data belonging to other accounts by modifying parameters sent in the HTTP request.

* **Target Goal:** Access Carlos's account page/data.
* **Vulnerability:** Insecure Direct Object References (IDOR)
* **Severity:** High

---

## Technical Analysis

### Vulnerability Explanation
Insecure Direct Object References occur when an application uses user-supplied input to directly access database records or objects without enforcing proper access control checks. 

In this lab:
1. The application references account profiles using an unencrypted, sequential parameter in the URL parameter: `?id=username`.
2. The backend server trusts the parameter value sent by the client without verifying whether the active authenticated session owns that requested resource.

---

## Step-by-Step Exploitation

### 1. Manual Exploitation (Burp Suite / Browser)
1. Log in to your provided account credentials.
2. Intercept the request to `/my-account` or inspect the page URL in the browser address bar.
3. Observe the URL parameter structure:
   ```http
   GET /my-account?id=your-username HTTP/1.1
   Host: target-lab-id.web-security-academy.net
   Cookie: session=YOUR_SESSION_COOKIE