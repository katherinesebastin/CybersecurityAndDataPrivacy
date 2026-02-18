### Objective   

The objective of this task was to evaluate the security of password storage in the Booking System Phase 2 application by attempting to recover user passwords from stored password hashes.  

### Observations  

After accessing the PostgreSQL database of the web application, we observed passwords were as 32 character hash values. This format is MD5 hashing. MD5 is not suitable for password storage because it is very fast and vulnerable to offline cracking attacks.  

### Attack Scenario   

Since we had access to the database and password hashes, this was an offline attack scenario.    
In an offline attack:  
- No login page is used  
- No account lockout occurs  

This increases the attacker’s advantage.  

### Cracking Method Used  

The stored MD5 hashes were tested using an online MD5 hash lookup website (CrackStation).  
Process:  
- Copy the MD5 hash from the database.  
- Submit the hash to the website.  
- The service compares the hash with large databases and known password datasets.  
- If a match is found, the original password is revealed.  

Because MD5 is widely used and many weak passwords are already known.  

### Cracked Passwords    

**User 1:** whatsupdoc@looneytunes.tv     
**Method:** Hash lookup (dictionary-based attack)  
**Result:** Password recovered - carrots123  
**Explanation:** The password was found in the cracking database, showing that it is commonly used.  
<img width="812" height="80" alt="Screenshot 2026-02-17 at 23 26 11" src="https://github.com/user-attachments/assets/494c7163-6359-4570-91e1-f8cce50dc31d" />  



**User 2:** doh@springfieldpower.net  
**Method:** Hash lookup  
**Result:** Password recovered - donuts4life  
**Explanation:** The password was found in the cracking database, showing that it is commonly used.  
<img width="812" height="80" alt="Screenshot 2026-02-17 at 23 26 26" src="https://github.com/user-attachments/assets/043f6416-6321-46cf-b2c8-aeba78f85636" />  



**User 3:** darkknight@gothamwatch.org  
**Method:** Hash lookup  
**Result:** Password recovered - iamvengeance  
**Explanation:**  The password was easily found due to its common usage.  
<img width="812" height="80" alt="Screenshot 2026-02-17 at 23 26 39" src="https://github.com/user-attachments/assets/e994fce9-3be5-42fb-9408-70a4fcfa50e1" />  



**User 4:** iamyourfather@deathstar.gov  
**Method:** Hash lookup  
**Result:** Password recovered - darkside42  
**Explanation:** The password was simple and present in public cracking databases.  
<img width="812" height="80" alt="Screenshot 2026-02-17 at 23 27 12" src="https://github.com/user-attachments/assets/043987e9-4803-4f18-854d-51dcc889e237" />



**User 5:** genius@starkindustries.com  
**Method:** Hash lookup  
**Result:** Password recovered - iamironman  
**Explanation:** The password was predictable and commonly used.   
<img width="812" height="80" alt="Screenshot 2026-02-17 at 23 28 01" src="https://github.com/user-attachments/assets/d9e6daa1-e6c1-4bf8-b73f-00322a7f8f6c" />  



### Analysis of Security Weakness  

Vulnerabilities identified:  
- Use of MD5 for password storage  
- Weak human generated passwords  
- Database access allows offline cracking  

MD5 is extremely fast, which allows an attacker to test millions or billions of passwords per second. If the database is leaked, weak passwords can be recovered easily.  

#### What is the main difference between Dictionary and Non-Dictionary attacks?  

A Dictionary attack uses a predefined list of possible passwords. It works well because many users choose predictable passwords.  
A Non-Dictionary attack (brute-force attack) tries every possible character combination within a given length and character set. It does not rely on common words but tests all possibilities.  

Main difference:  
- Dictionary attack → Faster against human passwords  
- Non-dictionary attack → Tries all combinations; slower but eventually successful  

#### What advantage does an attacker gain by having access to the system’s database with password hashes?  

When an attacker has access to the database, the attack becomes offline.  

Advantages:    
- Unlimited password attempts
- No account lockout
- No detection by the application  

This increases the possibility of successfully recovering passwords.

#### What concrete security benefits are achieved by using longer passwords?  

Longer passwords are harder to guess because every extra character makes the number of possible combinations grow exponentially.  

For example:  
- A 6 character lowercase password → 26⁶ combinations  
- A 12 character password using letters, numbers and symbols → 95¹² combinations  

Security benefits:  
- Much longer cracking time  
- Stronger resistance to brute-force attacks  
- Increased difficulty for dictionary-based attacks  
- More protection in offline attack scenarios  

Longer passwords require more computational effort to crack, making attacks harder.    
