# 1️⃣ Introduction      

**Tester(s):**      
- Name: Alena Genkinger, Katherine Sebastin      

**Purpose:**      
- To identify security vulnerabilities in the registration functionality.      

**Scope:**      
- Tested components: User registration    
- Exclusions: Authentication after login, authorization    
- Test approach: White-box      

**Test environment & dates:**      
- Start: 02.02.2026      
- End:  02.02.2026      
- Test environment details (OS, runtime, DB, browsers): Linux (Debian), Web application running on http://localhost:8001, PostgreSQL, Firefox    

**Assumptions & constraints:**      
- Testing was done in a local Docker environment        
- No changes were made to the application source code  
- Only automated scanning using OWASP ZAP was done       

---

# 2️⃣ Executive Summary    

**Short summary:**    
The security assessment identified multiple high and medium risk vulnerabilities in the registration functionality, like injection flaws and missing security protections.    

**Overall risk level:** High    

**Top 5 immediate actions:**      
1. Fix SQL Injection vulnerability in the registration   
2. Prevent Path Traversal through input validation    
3. Implement Anti-CSRF tokens for all forms    
4. Add missing security headers (CSP, X-Frame-Options)    
5. Improve error handling to prevent information disclosure   

---

# 3️⃣ Severity scale & definitions    

|  **Severity Level**  | **Description**                                                                                                              | **Recommended Action**           |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------------- | -------------------------------- |
|      🔴 **High**     | A serious vulnerability that can lead to full system compromise or data breach (e.g., SQL Injection, Remote Code Execution). | *Immediate fix required*         |
|     🟠 **Medium**    | A significant issue that may require specific conditions or user interaction (e.g., XSS, CSRF).                              | *Fix ASAP*                       |
|      🟡 **Low**      | A minor issue or configuration weakness (e.g., server version disclosure).                                                   | *Fix soon*                       |
| 🔵 **Info** | No direct risk, but useful for system hardening (e.g., missing security headers).                                            | *Monitor and fix in maintenance* |


---

# 4️⃣ Findings    

| ID | Severity | Finding | Description | Evidence / Proof |
|------|-----------|----------|--------------|------------------|
| F-01 | 🔴 High | SQL Injection | The username parameter in the registration is vulnerable to SQL Injection, allowing query manipulation and server errors | ZAP detected boolean-based SQL Injection and HTTP 500 errors |
| F-02 | 🔴 High | Path Traversal | User input in the registration is not properly validated, potentially allowing access to unintended file paths | ZAP Path Traversal alert on /register |
| F-03 | 🟠 Medium  | Absence of Anti-CSRF Tokens | The registration does not include an Anti-CSRF token, making it vulnerable to CSRF attacks | <form action="/register" method="POST"> without CSRF token |
| F-04 | 🟠 Medium | Missing Security Headers | Important headers like Content-Security-Policy and X-Frame-Options are not set, increasing XSS and clickjacking risks | ZAP header analysis |
| F-05 | 🟡 Low | Application Error Disclosure | Server returns detailed error responses (HTTP 500), which may reveal internal application details | HTTP/1.1 500 Internal Server Error |


---

> [!NOTE]  
> Include up to 5 findings total.    
> Keep each description short and clear.  

---

# 5️⃣ OWASP ZAP Test Report (Attachment)  

**Purpose:**  
- To provide a detailed automated vulnerability scan report generated using OWASP ZAP.     

---
📁 **Full report:**  
https://github.com/katherinesebastin/CybersecurityAndDataPrivacy/blob/main/BookingSystem-Phase1/zap_report_round1.md

---
