---
author: ariffinmzin
title: "Rules and Regulations for Faculty Server Usage"
date: 2025-05-20 12:00:00 +0800
categories: [guidelines, fyp]
tags: [server, UTHM, eduroam, rules]
pin: true
---


Welcome to the Faculty FYP Server! To ensure a fair, secure, and smooth experience for everyone, **all students must adhere to the following rules**. Access is a privilege, not a right—misuse will result in disciplinary action.

---

## 1. Access & Eligibility
- **Network Restriction**  
> The server is only reachable **on-campus** via **UTHM Wi-Fi** or **eduroam**.  
  {: .prompt-info } 
- **Account Ownership**  
  You may only access **your own** project directory.  
- **Maintenance Windows**  
  Scheduled downtime will be announced on this site 48 hours in advance. Plan your work accordingly.

---

## 2. Supported Development Stack
You are free to build within the following tech stack **only**:
- **Frontend:** HTML5, CSS3, JavaScript  
- **Backend:** PHP 8.4  
- **Database:** MySQL / MariaDB  

> _Other frameworks or languages (Laravel, Node.js, Python, Ruby, etc.) are currently  **not** supported on this server._
{: .prompt-tip } 

---

## 3. Database Naming Conventions 
- **Database name:** `<matric>`  
- **MySQL/MariaDB username:** `<matric>`  
- **MySQL/MariaDB password:** `<matric>`

---

## 4. Prohibited Actions & Misuse
Any of the following will be treated as **severe misconduct**:
- 🚫 Uploading or hosting **illegal content** other than your FYP  
- 🚫 Attempting to access or modify **other students’** files or databases  
- 🚫 Installing or running **unapproved services**
- 🚫 Cracking, brute-forcing, or scanning the server/network  
- 🚫 Sharing your credentials or letting others use **your** account  

> _**Disciplinary Measures:** Accounts found abusing the server will be suspended and reported to the faculty misconduct committee._
{: .prompt-danger } 

---

## 5. Security & Best Practices
- 🔑 **Strong Passwords:** Your DB password is initially your matric, but you may change it—avoid common words or patterns.  
- 🔄 **Backups:** Keep a local copy of your `.sql` export and project files.  
- 🔍 **Error Logs:** Check `/var/log/nginx/` or `/var/log/httpd/` if you hit “500” errors.  
- 📡 **HTTPS Only:** Always use `https://10.65.200.7/<your-matric>` after trusting our self-signed cert.  
- 🛡️ **Updates:** We manage system updates centrally. Do not attempt to upgrade PHP, MySQL, or system packages.

---

## 6. Support & Contact
If you encounter issues or need an exemption, please:
1. Open a ticket at **IT Helpdesk** (Lab 3, FSKTM).  
2. Email **itlab@uthm.edu.my** with subject `[FYP SERVER] YourMatric YourIssue`.

---

> By using the Faculty FYP Server, you agree to abide by these rules. Let’s keep our environment professional, secure, and collaborative. Good luck with your project!  