# FortiWeb RCE Toolkit 🔐

Automated proof-of-concept tool for **CVE-2025-25257** in Fortinet FortiWeb – featuring **reverse shell**, **exfiltration**, **persistence**, and **cleanup**. **Only for lab/testing environments. DO NOT USE in production.**

---

## ⚙️ Features

- ✔️ Pre-authenticated detection of vulnerable FortiWeb versions  
- 🐚 Reverse shell (bash) via `/cgi-bin/shell.sh`  
- 📤 Encrypted data exfiltration to `/tmp/exfil.txt` (Base64-encoded)  
- 🕒 Persistence via cron job (`/etc/cron.d/sys`)  
- 🧹 Full cleanup after use (removes shell + cron + SQL traces)  
- 🔒 Only active while listener runs and cleanup is triggered  

---

## 📋 Requirements

- Python 3.6+  
- `requests` library:  
  ```bash
  pip install requests
