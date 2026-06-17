- Before we start learning about `deobfuscation`, we must first learn about `code obfuscation`. 
- Without understanding how code is obfuscated, we may not be able to successfully deobfuscate the code, especially if it was obfuscated using a custom obfuscator.


# What is obfuscation
- **Obfuscation purpose:** makes source code hard for humans to read while preserving runtime behavior; may slow performance.
- **How it’s done:** typically with an automated obfuscation tool that rewrites code into a more confusing form.
- **Dictionary technique:** many obfuscators create a dictionary of tokens (words/symbols) and rebuild the original code at execution time by referencing that dictionary.
- **Common in interpreted languages:** interpreted languages (JavaScript, Python, PHP) run from source; JavaScript is delivered to clients in cleartext, so obfuscation is frequently applied to hide logic in browser-executed code.
- **Server-side vs client-side:** Python and PHP are usually server-side (hidden from users), whereas JavaScript runs client-side (visible to users), making obfuscation especially useful for JS.
- **Example tools:** online JS obfuscators can transform readable JS into encoded/packed forms (e.g., tools like the one linked).


# Use Cases
- **Reasons for obfuscation:**
    - Protect original code from being copied or reused without permission.
    - Make reverse engineering more difficult.
    - Add a basic security layer around sensitive logic like authentication or encryption.
- **Important note:**
    - Performing **authentication or encryption on the client-side** is insecure and not recommended, as the code is exposed to users.
- **Malicious use:**
    - Attackers often obfuscate scripts to **evade detection** by Intrusion Detection and Prevention Systems (IDPS).
- **Next step:**
    - Learn to obfuscate simple JavaScript code and observe differences in behavior **before and after obfuscation**.