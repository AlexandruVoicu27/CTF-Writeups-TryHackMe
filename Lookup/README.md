**DESCRIPTION**

  Lookup offers a treasure trove of learning opportunities for aspiring hackers. This intriguing machine showcases various real-world vulnerabilities, ranging from web application weaknesses to privilege escalation techniques. By exploring and exploiting these vulnerabilities, hackers can sharpen their skills and gain invaluable experience in ethical hacking. Through "Lookup," hackers can master the art of reconnaissance, scanning, and enumeration to uncover hidden services and subdomains. They will learn how to exploit web application vulnerabilities, such as command injection, and understand the significance of secure coding practices. The machine also challenges hackers to automate tasks, demonstrating the power of scripting in penetration testing.﻿

**HOW TO SOLVE?**
Used nmap with server detection to find something and found the site http://lookup.thm.
<img width="1305" height="792" alt="image" src="https://github.com/user-attachments/assets/84a1f50c-1317-4228-96ea-71d53d42d874" />

Mapped it so I can open it.
<img width="2553" height="1373" alt="image" src="https://github.com/user-attachments/assets/96a37486-fcb0-4d09-963c-873035d2668b" />

Brute forced the username and the password with Zaproxy and found jose: password123
<img width="2561" height="1263" alt="image" src="https://github.com/user-attachments/assets/6ad9a110-eedd-44ad-abdd-84ad424559cb" />

In the Credentials files found an username and a password that I tried using ssh but didnt work, but I found the vulnerabilites on elfinder for the specific version that it works on.
<img width="2484" height="1309" alt="image" src="https://github.com/user-attachments/assets/6399f16c-a592-4aa4-906e-1edfb329cca1" />

<img width="788" height="300" alt="image" src="https://github.com/user-attachments/assets/926853df-354f-47a8-ab72-60f36277de6b" />

Used msfconsole to search for the vulnerabilites.
<img width="1929" height="210" alt="image" src="https://github.com/user-attachments/assets/e15c3a60-bd6a-4c4c-a230-8d535993e1f0" />

I performed a PATH hijacking attack by creating a malicious id script in the writable /dev/shm directory and prepending that directory to my PATH environment variable, which tricked the /usr/sbin/pwm binary into executing my script and dumping the contents of the restricted passwords file.

<img width="837" height="715" alt="image" src="https://github.com/user-attachments/assets/f0e703ff-825e-464d-b7ae-92cf08c56394" />

Once I opened it tried some of the passwords for username think and found that the correct one was: josemario.AKA(think)
After this was easy to find the flags for user and the root.
<img width="1096" height="686" alt="image" src="https://github.com/user-attachments/assets/3cc65af8-9dea-4556-ad81-c951508457e7" />
<img width="1144" height="299" alt="image" src="https://github.com/user-attachments/assets/3c0617b6-da08-4607-a101-85c5e15803a5" />


**User Flag:** `38375fb4dd8baa2b2039ac03d92b820e`
**Root Flag** `5a285a9f257e45c68bb6c9f9f57d18e8`

