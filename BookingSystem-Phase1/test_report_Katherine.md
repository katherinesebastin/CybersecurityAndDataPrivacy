# 1️⃣ Introduction  

**Tester(s):**    
- Name: Katherine Sebastin    

**Purpose:**    
- To identify vulnerabilities in the user registration of the booking system      

**Scope:**    
- Tested components: User registration page, database, input validation    
- Exclusions: Login, session management, resource booking    
- Test approach: Gray-box    

**Test environment & dates:**    
- Start: 31.01.2026    
- End:  31.01.2026    
- Test environment details (OS, runtime, DB, browsers): macOS, Docker containers (PostgreSQL + Web App), Chrome    

**Assumptions & constraints:**    
- Access to the local lab environment      
- No real user data used      

---

# 2️⃣ Executive Summary  

**Short summary:**  
The registration validates some inputs (empty fields, email format, username length) but has flaws like weak password acceptance, lack of age validation, role manipulation and missing security features (captcha, confirm password).  

**Overall risk level:** High  

**Top 5 immediate actions:**    
1. Add age validation for registrants  
2. Restrict role assignment to administrators  
3. Implement password strength requirements and confirm password field  
4. Add captcha to prevent automated registrations  
5. Ensure proper input sanitization and hashing of passwords in the database  

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
| F-01 | 🔴 High | Role manipulation | Users can set their role to 'administrator' during registration | Registered 'test@test.com' with role administrator, shown in DB table booking_users |
| F-02 | 🔴 High | Missing age validation | Users can register with any birthdate, including underage | Birthdate field accepted 31.01.2026 |
| F-03 | 🔴 High | Weak password | Password field accepts weak passwords (e.g., efgh) with no warnings | Registration of 'test@test.com' succeeded with weak password |
| F-04 | 🟠 Medium | Missing confirm password & captcha | No confirm password field or captcha, allowing accidental or automated registrations | UI observation during manual testing |


---

> [!NOTE]
> Include up to 5 findings total.   
> Keep each description short and clear.

---

# 5️⃣ OWASP ZAP Test Report (Attachment)

**Purpose:**  
- Attach or link your OWASP ZAP scan results (Markdown format preferred).

---

**Instructions:**
1. Check lecture recordings
2. Save the report as `zap_report_round1.md` and link it below.

---
> [!NOTE]
> 📁 **Attach full report:** → `check itslearning` → **Add a link here**

---
