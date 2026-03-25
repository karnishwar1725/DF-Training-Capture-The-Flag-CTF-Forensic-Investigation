
🕵️ DF Training: Capture The Flag (CTF) Forensic Investigation

⸻

📌 Overview

This project documents a digital forensic Capture-The-Flag (CTF) investigation performed on a vulnerable virtual machine.

The objective was to:
	•	Identify and extract 5 hidden flags
	•	Use multiple forensic and penetration testing techniques
	•	Combine findings to gain root access

⸻

🎯 Objectives
	•	Perform investigation in an isolated virtual lab
	•	Enumerate services and vulnerabilities
	•	Extract hidden data using:
	•	Hash cracking
	•	FTP analysis
	•	Directory brute forcing
	•	Port scanning
	•	Achieve privilege escalation (root access)

⸻

🧪 Lab Environment

🖥️ Virtual Machines
	•	Kali Linux (Attacker machine)
	•	DF Training Server (Ubuntu-based)

🔒 Network Configuration
	•	Host-only network (isolated environment)
	•	Target IP: 192.168.56.101

👉 As described in the setup section, both VMs were configured in the same subnet to ensure connectivity while maintaining isolation  ￼

⸻

🧠 Challenge Summary
	•	5 flags hidden across the system
	•	First 4 flags = 2-digit numbers (00–99)
	•	Final flag requires:
	•	Combining previous flags → login password

⸻

🚩 Flag Breakdown

⸻

🔐 Flag 1 – Hash Cracking
	•	Given: MD5 + SHA1 hashes
	•	Approach:

echo -n XX | md5sum
echo -n XX | sha1sum


	•	Brute-forced values from 00–99

✅ Flag 1: 22

👉 Hash matching confirmed correct value through both algorithms  ￼

⸻

📂 Flag 2 – FTP Investigation
	•	Discovered via:

nmap 192.168.56.101


	•	FTP (Port 21) open
	•	Credentials:

Username: test
Password: test



Key Findings:
	•	Fake flag in /directory
	•	Real flag in /files/FLAG2.txt

✅ Flag 2: 44

👉 FTP directory structure included misleading files and required careful inspection  ￼

⸻

🗂️ Flag 3 – Hidden Directory Discovery
	•	Tool used:

dirb http://192.168.56.101/



Discovery Path:

/php/readme/FLAG/flag3.txt

✅ Flag 3: 66

👉 Hidden directories were not linked and required brute-force discovery  ￼

⸻

🌐 Flag 4 – Hidden Web Service
	•	Full port scan:

nmap -p- 192.168.56.101



Key Discovery:
	•	HTTP service on port 14545

Technique:
	•	Inspect webpage source (Ctrl + U)
	•	Flag hidden in HTML

✅ Flag 4: 88

👉 Non-standard port scanning revealed hidden services missed by default scans  ￼

⸻

🔓 Flag 5 – Root Access
	•	Combined password:

22 + 44 + 66 + 88 → 22446688


	•	Login:

Username: root
Password: 22446688



Final Location:

/subfolder/FLAG

✅ Final Flag: 99

👉 Root access enabled full system inspection and final flag extraction  ￼

⸻

🧾 Final Flag Summary

Flag	Value
Flag 1	22
Flag 2	44
Flag 3	66
Flag 4	88
Flag 5	99


⸻

🛠️ Tools & Commands Used

🔧 Tools
	•	Kali Linux
	•	Nmap
	•	FTP
	•	DIRB
	•	Linux CLI

💻 Key Commands

ifconfig
nmap 192.168.56.101
nmap -p- 192.168.56.101
ftp 192.168.56.101
dirb http://192.168.56.101/
cat FLAG
cd subfolder


⸻

🧠 Key Learnings
	•	Importance of enumeration before exploitation
	•	Real-world use of:
	•	Network scanning
	•	Service exploitation
	•	Directory brute forcing
	•	Recognizing:
	•	Fake/misleading artifacts
	•	Hidden services
	•	Combining small findings to achieve full system compromise

⸻

🚀 How to Reproduce
	1.	Import OVA into VirtualBox
	2.	Configure both VMs to Host-only network
	3.	Identify target IP using:

ifconfig


	4.	Perform:
	•	Nmap scan
	•	FTP login
	•	Directory brute forcing
	•	Port scanning
	5.	Combine flags → login as root
