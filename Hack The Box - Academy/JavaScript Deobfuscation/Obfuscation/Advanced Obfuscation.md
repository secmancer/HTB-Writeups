- So far, we have been able to make our code obfuscated and more difficult to read.
- However, the code still contains strings in cleartext, which may reveal its original functionality.
- In this section, we will try a couple of tools that should completely obfuscate the code and hide any remnants of its original functionality.


# Obfuscator
- Used **obfuscator.io** and set **String Array Encoding → Base64** before obfuscating.
- Pasted `console.log('HTB JavaScript Deobfuscation Module');` and clicked **Obfuscate**.
- Output is a heavily transformed script that:
    - Replaces strings with entries in an array (`var _0x1ec6 = [...]`).
    - Performs an **array rotation/shift** bootstrapping step (self-invoking function that shifts the array).
    - Exposes a lookup function (`_0x14f8`) that converts an index (like `'0x0'`, `'0x1'`) to the decoded string.
    - Includes an internal **Base64 → decoded string** routine (`_0x3f720f` + wrapper) and a `%xx` → `decodeURIComponent` step to recover original text.
    - Caches decoded values (`_0x14f8['qHtbNC']`) so repeated lookups are fast.
- Final call becomes `console[_0x14f8('0x0')](_0x14f8('0x1'));` — functional but unreadable.
- Behavior preserved: running the obfuscated script (e.g., in JSConsole) still prints the original message.
- Takeaway/tips: tweak obfuscator settings for stronger transformations, then always **test the obfuscated output** in a safe sandbox (like JSConsole or an isolated VM) to confirm functionality.


# More Obfuscation
- Extremely aggressive obfuscation can use JavaScript tricks (like `![]`, `+[]`, `[][[]]`, etc.) to build strings and identifiers purely from boolean/array expressions.
- Such scripts become **nearly unreadable** but remain fully functional when executed.
- You can **test** these on a sandboxed console (e.g., JSConsole) to confirm they still perform the original action.
- Heavily obfuscated code may be **very long** and **slow to execute/compile**, demonstrating the performance cost of obfuscation.
- Some obfuscators (JJEncode, AAEncode, etc.) produce extreme encodings that significantly **increase runtime overhead** — avoid them unless there’s a strong reason (e.g., bypassing filters).
- Obfuscation trade-offs: stronger hiding vs. slower execution, harder debugging, and larger payloads.
- Always **test obfuscated output** in a safe sandbox/VM to verify functionality and measure performance impact.