## Recon & scanning
- Quick TCP discovery: `nmap -sC -sV -oA quick <IP>` (service/version + default scripts).
- Full port scan: `nmap -p- -T4 -oA full <IP>` then targeted service scans on discovered ports: `nmap -p<ports> -sC -sV -oA svc <IP>`.


## Web footprinting (if web ports found)
- Fingerprint: `whatweb <IP>:<port>` or browse in browser.
- Directory/file bruteforce: `gobuster dir -u http://<host> -w /path/wordlist -x php,txt,html` (adjust extensions).
- Add host entry to `/etc/hosts` only if needed: `<IP> example.local` (optional).


## Vulnerability research
- For discovered software/versions use **Searchsploit** or search manually for public exploits and PoCs.
- Check CVEs, common misconfigurations, and default creds for identified services.


## Gaining a foothold
- Try both paths:
    - **Manual**: craft an exploit or use discovered misconfig/config leakage to get shell.
    - **Metasploit**: import exploit/module, set RHOST/RPORT/PAYLOAD, test in a controlled way.
- After initial shell, upgrade to a proper interactive TTY:
    - `python3 -c 'import pty; pty.spawn("/bin/bash")'` (or `python -c ...` depending on system).
    - Then `ctrl-z` and `stty raw -echo; fg` to fully interact if needed.


## Post-foothold enumeration
- Manual file system checks: `id`, `uname -a`, `whoami`, `hostname`, `cat /etc/passwd`, `ps aux`, `sudo -l`.
- Search for credentials, config files, keys, scheduled tasks, and world-writable files.
- Automated helpers: run **LinEnum** and **LinPEAS** locally (download/curl to target) and review output carefully.


## Privilege escalation (after foothold)
- Use LinEnum / LinPEAS to highlight vectors; filter results for likely candidates.
- Focus on two well-known escalation classes (look for both):
    1. **Sudo misconfigurations / weak sudo rules** — `sudo -l` reveals binaries run as root.
    2. **SUID binaries / vulnerable services / kernel exploits / cron jobs** — check `find / -perm -4000 -type f 2>/dev/null`, `crontab -l`, `/etc/cron.*`, and service configs.
- Validate any chosen technique manually before running noisy exploits.


## Organization & workflow
- Keep notes offline (IP, open ports, services, creds, exploits tried, successes/failures).
- Map attack paths: which initial access leads to which escalation paths — prioritize least noisy and highest success probability.
- Iteratively re-scan and re-enumerate after each discovery.


## Safety & etiquette
- Don’t use walkthroughs while attempting a live box (unless allowed).
- Ask for help only following best practices (be specific, non-spoiler).
- Have fun, learn from failures, and always document what you learned.


# Questions
- Spawn the target, gain a foothold and submit the contents of the user.txt flag.
	- 7002d65b149b0a4d19132a66feed21d8
- After obtaining a foothold on the target, escalate privileges to root and submit the contents of the root.txt flag.
	- f1fba6e9f71efb2630e6e34da6387842

# Notes
- Ran nmap, only found port 22 and 80. Not much of interest given from here.
- Visting the site, we are told it's using GetSimple CMS.
- Went ahead and ran gobuster, and was able to find these subdirectories:
```
/data                 (Status: 301) [Size: 313] [--> http://10.129.42.249/data/]  
/admin                (Status: 301) [Size: 314] [--> http://10.129.42.249/admin/]  
/plugins              (Status: 301) [Size: 316] [--> http://10.129.42.249/plugins/]  
/theme                (Status: 301) [Size: 314] [--> http://10.129.42.249/theme/]  
/backups              (Status: 301) [Size: 316] [--> http://10.129.42.249/backups/]  
Progress: 68703 / 220557 (31.15%)
```
- I was able to confirm it has version 3.3.15 installed.
- Looking through searchsploit, I was able to find a remote code execution vulnerability, and was able to confirm the GetSimple CMS instance was indeed vulnerable.
- I was able to get remote code execution.
- I then upgraded my shell using python and bash:
	- python3 -c 'import pty; pty.spawn("/bin/bash")'
- Was able to upgrade it and read out the user flag.
- After that, I need to priv-sec to the root user.
- I first started with opening up an HTTP server where I keep my resources at, and then downloaded an ran a copy of LinEnum onto the target.
- It seems that we can read and write to password/shadow files, which means we can take advantage of that:
```
[-] Can we read/write sensitive files:  
-rw-r--r-- 1 root root 1813 Feb  9  2021 /etc/passwd  
-rw-r--r-- 1 root root 826 Feb 16  2021 /etc/group  
-rw-r--r-- 1 root root 581 Dec  5  2019 /etc/profile  
-rw-r----- 1 root shadow 1051 Feb  9  2021 /etc/shadow
```
- We also have full access to php. Maybe we can do something with this...
- Looking around online, we can use this snippet to upgrade our shell. Example used sh, but I went ahead and did bash so that I could have the nice features with it:
```
sudo php -r "system('/bin/bash');"
```
- And... it worked!
```
root@gettingstarted:/tmp# id  
id  
uid=0(root) gid=0(root) groups=0(root)
```
- From here, we are able to read out the root flag!
- Boom, we have pwned the box!