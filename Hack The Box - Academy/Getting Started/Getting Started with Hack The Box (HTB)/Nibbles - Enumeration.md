- **Retired Boxes & Walkthroughs**
    - 201 standalone retired boxes available with VIP; each has an official HTB walkthrough, plus many 3rd-party blogs/videos.
- **Target for Practice: Nibbles**
    - **OS**: Linux | **Difficulty**: Easy (20 pts) | **Release**: 13 Jan 2018 | **IP**: `10.10.10.75`
    - **Creator**: mrb3n | **User path**: Web
    - **Priv-esc themes**: World-writable file / sudoers misconfig
    - **Refs**: Ippsec video & 0xdf walkthrough (for after-action learning)
- **Pentest Approaches (context)**
    - **Black-box**: minimal knowledge; heavy recon; most like real attacks but can miss issues.
    - **Grey-box**: some info (IPs, low creds, diagrams); less recon, more focused exploitation.
    - **White-box**: full access (code, admin creds, diagrams); most comprehensive.
- **Nmap Strategy (enumeration is iterative)**
    1. **Quick scan**: `nmap -sV --open -oA nibbles_initial_scan <IP>` (top 1000 ports, service versions).
        - Trick: `nmap -v -oG -` (with no target) shows which ports a scan profile would hit.
    2. **Full TCP sweep**: `nmap -p- --open -oA nibbles_full_tcp_scan <IP>` (find non-standard ports).
    3. **Targeted scripts**: `nmap -sC -p 22,80 -oA nibbles_script_scan <IP>`; optionally `--script http-enum` for web dirs.
    4. **Banner grab (cross-check)**:
        - SSH: `nc -nv <IP> 22` → `OpenSSH_7.2p2 Ubuntu-4ubuntu2.8`
        - HTTP: `nc -nv <IP> 80` → confirms web service
- **Observed Results (sample run vs. practice host)**
    - Open ports: **22/tcp (SSH)**, **80/tcp (HTTP/Apache on Ubuntu)**  
    - `http-title`: none; `http-enum`: no obvious finds
    - Full port scan: no additional TCP ports
    - Outputs saved as: `*.gnmap`, `*.nmap`, `*.xml` for later parsing/reporting
- **Process/Notes Discipline**
    - Save all scan outputs (`-oA`), keep detailed, time-stamped notes of recon and exploitation steps.
    - This habit speeds reporting, preserves evidence, and helps during incidents/outages.


# Questions
- Run an nmap script scan on the target. What is the Apache version running on the server? (answer format: X.X.XX)
	- I'll use rustscan, which allows for the use of nmap scripts, but is faster at scanning.
	- Went ahead and upped the ulimit as well.
	- However, I was able to get the relevant Apache version, which is 2.4.18
	- Answer: 2.4.18


# Rustscan Command
```
rustscan -a 10.129.240.33 --ulimit 5000 -- -sV
```
