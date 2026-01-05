# Honeypot Project

## Overview
This project implements a **multi-service honeypot** that simulates vulnerable **HTTP, SSH, and FTP** services.  
The purpose is to attract attackers, log malicious behavior, and study common attack techniques such as brute force, SQL injection, and path traversal—without exposing a real system.

---

## Requirements
- Linux system
- Python 3
---

## Installation

Clone the repository:
```bash
git clone https://github.com/ayazrrouni/honey.git
cd honeypot
pip install flask paramiko
```
##Running the Honeypot

Start the honeypot (root privileges required):
sudo python3 main.py

Expected output:
```bash
[+] HTTP Honeypot listening on port 80
[+] SSH Honeypot listening on port 2222
```
#Testing the Services
1) SSH Honeypot

Connect to the SSH honeypot:
```bash
ssh root@127.0.0.1 -p 2222
```
Enter any password

Try common commands:
```bash
ls
pwd
id
sudo -l
```
All commands are simulated and logged.

#2) HTTP Honeypot
Fake Admin Login

Accepts any username and password

Redirects to a fake admin dashboard

Used to observe attacker behavior

Test in a browser:
```bash
http://127.0.0.1
http://127.0.0.1/admin
http://127.0.0.1/admin/dashboard
```

#Brute Force Simulation

-Simulates a vulnerable login endpoint

-Always returns invalid credentials

-Logs every attempt
```bash
http://127.0.0.1/bruteforce
```

#Path Traversal / LFI Simulation

Simulates a Local File Inclusion vulnerability

Returns a fake /etc/passwd file

Detects directory traversal attempts
```bash
http://127.0.0.1/download?file=../../etc/passwd
```

#SQL Injection Honeypot

Dedicated endpoint for SQL injection testing

Detects common SQL injection patterns

Returns realistic SQL error messages

No real database is used
```bash

http://127.0.0.1/sql_login
```


HTTP Attack Logs

All detected HTTP attacks are logged in:
```bash

logs/attacks.log
```
#3) FTP Honeypot

Start Metasploit:
```bash
msfconsole -q
```

Use the vsFTPd backdoor exploit:
```bash
use exploit/unix/ftp/vsftpd_234_backdoor
set RHOSTS 127.0.0.1
nc 127.0.0.1 6200
```
Test commands:

```bash
ls
pwd
id
uname
```

Disclaimer

>This project is for educational and research purposes only.
>Do not deploy on public networks or use for illegal activities.
