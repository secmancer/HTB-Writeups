- After completing the prior exercise, an encoded text block was returned.
- Example request shown: `curl http://SERVER_IP:PORT/serial.php -X POST -d "param1=sample"`.
- The response included the Base64-looking string: `ZG8gdGhlIGV4ZXJjaXNlLCBkb24ndCBjb3B5IGFuZCBwYXN0ZSA7KQo=`.
- This illustrates a common obfuscation tactic: embedding encoded text that is decoded at runtime.
- Obfuscated code is used to make content harder for humans to read and harder for detection systems to flag.
- The text notes three common encoding methods used in obfuscation: **base64**, **hex**, and **rot13**.


# Base64
- **Why base64 is used:** converts any input (including binary) into a limited character set to avoid special characters — output uses alphanumeric characters plus `+` and `/`.
- **Distinctive feature:** base64 strings are easy to spot because they contain only letters, numbers, `+`/`/`, and often trailing = padding.
- **Padding rule:** base64 output length is a multiple of 4; = characters are added as padding when needed.
- **Spotting tip:** look for long runs of alphanumeric characters ending with one or more = — a strong sign of base64.
- **Encode example (Linux):** `echo https://www.hackthebox.eu/ | base64` → `aHR0cHM6Ly93d3cuaGFja3RoZWJveC5ldS8K`
- **Decode example (Linux):** `echo aHR0cHM6Ly93d3cuaGFja3RoZWJveC5ldS8K | base64 -d` → `https://www.hackthebox.eu/`


# Hex
- **What hex encoding is:** represents each character as its ASCII value in hexadecimal (e.g., `a` → `61`, `b` → `62`, `c` → `63`).
- **Where to check ASCII values:** use `man ascii` on Linux to view the full ASCII table.
- **Spotting hex:** hex strings use only the characters `0-9` and `a-f` (lowercase typically), making them easy to spot.
- **Encode (Linux):** `echo https://www.hackthebox.eu/ | xxd -p` → `68747470733a2f2f7777772e6861636b746865626f782e65752f0a`
- **Decode (Linux):** `echo 68747470733a2f2f7777772e6861636b746865626f782e65752f0a | xxd -p -r` → `https://www.hackthebox.eu/`


# Caesar/Rot13
- **What Caesar cipher is:** shifts each letter by a fixed number (e.g., `a`→`b`, `b`→`c` for shift 1).
- **Rot13 variant:** shifts letters by 13 places — the most common Caesar cipher version.
- **Spotting Caesar/Rot13:** text appears random but keeps recognizable structure (e.g., `http://www` → `uggc://jjj`).
- **Rot13 Encode (Linux):**  
    `echo https://www.hackthebox.eu/ | tr 'A-Za-z' 'N-ZA-Mn-za-m'` → `uggcf://jjj.unpxgurobk.rh/`
- **Rot13 Decode (Linux):** same command works both ways → `https://www.hackthebox.eu/`
- **Alternative option:** use an online ROT13 encoder/decoder tool.


# Other Types of Encoding
- There are many (hundreds) of other encoding methods beyond base64/hex/rot13 — some are obscure and require experience to recognize.
- When you encounter an unknown encoded string: first try to identify the encoding type, then search for tools or online decoders that handle that encoding.
- Automated helpers (example: **Cipher Identifier**) can often guess the encoding — try your encoded examples with such tools to see if they correctly identify them.
- Remember the difference between **encoding** and **encryption**: encoding transforms data into a different representation (no secret required), while encryption uses a key — if the decryption key isn’t present, reversing encrypted data may be infeasible.
- Many obfuscation tools mix encoding and encryption; if a key isn’t stored in the script, deobfuscation can be significantly harder.


# Questions
- Using what you learned in this section, determine the type of encoding used in the string you got at previous exercise, and decode it. To get the flag, you can send a 'POST' request to 'serial.php', and set the data as "serial=YOUR_DECODED_OUTPUT".
	- First, the post request:
		- curl -s http://83.136.250.6:50357/serial.php -X POST
	- We then get the following:
		- N2gxNV8xNV9hX3MzY3IzN19tMzU1NGcz
	- Now, we need to decode it.
	- I tried base64 first, and that ended up working:
		- Command: echo N2gxNV8xNV9hX3MzY3IzN19tMzU1NGcz | base64 -d
		- Response: 7h15_15_a_s3cr37_m3554g3
	- Now, we need to send that with another POST request:
		- curl -s http://83.136.250.6:50357/serial.php -X POST -d "serial=7h15_15_a_s3cr37_m3554g3"
	- We then get out flag:
		- HTB{ju57_4n07h3r_r4nd0m_53r14l}