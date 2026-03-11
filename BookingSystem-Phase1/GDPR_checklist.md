# GDPR Compliance Checklist – Web-based Booking System

| **Result** | **Personal data mapping and minimization** |
| :----: | :--- |
| ✅ | Have all personal data collected and processed in the system been identified? (e.g., name, email, age, username) |
| ✅ | Have you ensured that only necessary personal data is collected (data minimization)? |
| ✅ | Is user age recorded to verify that the booker is over 15 years old? |

---

| **Result** | **User registration and management** |
| :----: | :--- |
| ❌ | Registration form does not show GDPR consent (no privacy policy checkbox)|
| ⚠️ | Users can view data, but editing/deleting is not possible |
| ✅ | Is there a mechanism for the administrator to delete a reserver in accordance with the "right to be forgotten"? |
| ✅ | Is underage registration (under 15 years) and booking functionality restricted? |

---

| **Result** | **Booking visibility** |
| :----: | :--- |
| ✅ | Are bookings visible to non-logged-in users only at the resource level (without any personal data)? |
| ✅ | Is it ensured that names, emails, or other personal data of bookers are not exposed publicly or to unauthorized users? |

--- 

| **Result** | **Access control and authorization** |
| :----: | :--- |
| ⚠️ | Users can modify bookings and administrators cannot add bookings, so booking management is not completely restricted |
| ✅ | Is the system using role-based access control (e.g., reserver vs. administrator)? |
| ⚠️ | Admin privileges exist, but there is no proof preventing misuse of personal data |

---

| **Result** | **Privacy by Design Principles** |
| :----: | :--- |
| ✅ | Has Privacy by Default been implemented (e.g., collecting the minimum data by default)? |
| ✅ | Are logs implemented without unnecessarily storing personal data? |
| ✅ | Are forms and system components designed with data protection in mind<br> (e.g., secured login, minimal fields)? |

---

| **Result** | **Data security** |
| :----: | :--- |
| ✅ | Are CSRF, XSS, and SQL injection protections implemented? |
| ✅ | Are passwords securely hashed using a strong algorithm (e.g., bcrypt, Argon2)? |
| ⚠️ | Backup and recovery policy is not documented or visible |
| ⚠️ | Hosting location is not specified, so EU data center compliance cannot be verified |

---

| **Result** | **Data anonymization and pseudonymization** |
| :----: | :--- |
| ✅ | Is personal data anonymized where possible? |
| ⚠️ | Pseudonymization techniques cannot be verified |

---

| **Result** | **Data subject rights** |
| :----: | :--- |
| ❌ | Users cannot download or request all personal data related to them |
| ❌ | No interface exists for users to request deletion of their personal data |
| ❌ | Users cannot withdraw consent for data processing |

---

| **Result** | **Documentation and communication** |
| :----: | :--- |
| ❌ | Privacy policy page does not exist and it is not accessible in the application |
| ⚠️ | No documented practices available for administrators/developers regarding data protection |
| ⚠️ | No documented data breach response process is available |

---

**Symbols used:**  
✅ Pass (a note can be added)  
❌ Fail (a note can be added)  
⚠️ Attention (a note can be added)
