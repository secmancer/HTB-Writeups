- Now that we understand how code obfuscation works let's start our learning towards deobfuscation. 
- Just as there are tools to obfuscate code automatically, there are tools to beautify and deobfuscate the code automatically.


# Beautify
- Minified JavaScript is single-line, hard-to-read code; **beautifying** restores indentation but doesn’t remove obfuscation.
- Browser devtools can pretty-print minified scripts (Firefox: **Ctrl+Shift+Z** → open file → click `{ }` “Pretty Print”).
- Example workflow: open `secret.js` in DevTools, use the pretty-print button to get readable formatting.
- Online or editor tools (Prettier, Beautifier) also reformat JS into readable indentation and line breaks.
- Example obfuscated/minified snippet shown uses an `eval(function(p,a,c,k,e,d){...})` packer — prettifying makes structure visible but not the original logic.
- Beautifying helps by making the code structure and control flow visible, but **does not deobfuscate** renamed identifiers, encoded strings, or eval-packed payloads.
- To fully understand obfuscated scripts you need **deobfuscation tools and techniques** (iterative unpacking, replacing `eval`, dynamic debugging, etc.).
- Always use a **safe sandbox/VM** when running unknown obfuscated code while testing and deobfuscating.


# Deobfuscate
- Use online **deobfuscators** (example: UnPacker at `matthewfl.com/unPacker.html`) to automatically unpack many packed/obfuscated JS payloads.    
- **Paste carefully** — avoid leading empty lines (they can break some unpackers).
- UnPacker can recover readable code from packers, turning `eval(function(p,a,c,k,e,d){...})` into understandable functions (e.g., `function generateSerial() { ... xhr.open("POST", "/serial.php", true); xhr.send(null); }`).
- A simple manual unpacking trick: **replace the outer `eval(...)` with `console.log(...)`** (or breakpoint before eval) so the intermediate decoded string is printed rather than executed; then prettify that string.    
- Post-unpack steps: pretty-print the result, search for important strings/endpoints/flags, rename confusing identifiers to meaningful names, and step through with a debugger if needed.
- Always run unknown/untrusted code in a **sandboxed environment (VM/container/devtools)** to avoid accidental execution of malicious payloads.
- If UnPacker fails, try iterative approaches and other tools (JS beautifiers, AST parsers, or dynamic debugging) — some obfuscation layers must be removed one at a time.


# Reverse Engineering
- Automated deobfuscators work well for common packers/encoders, but their effectiveness drops as obfuscation complexity increases.
- Custom or heavily layered obfuscation can defeat automated tools — manual analysis becomes necessary.
- Manual reverse-engineering requires understanding the obfuscation technique and peeling layers one-by-one.
- Expect to use a mix of static analysis (beautifiers, AST inspection) and dynamic techniques (intercepting `eval`, runtime debugging, logging decoded payloads).
- Look for custom encodings, unusual control-flow tricks, or bespoke string mangling that standard tools won’t recognize.
- Manual work is slower and more error-prone, so keep experiments isolated in a sandbox/VM to avoid executing malicious code.
- Advanced deobfuscation and reverse-engineering are specialized skills — consider learning structured courses or modules (e.g., Secure Coding 101) for deeper coverage.


# Questions
- Using what you learned in this section, try to deobfuscate 'secret.js' in order to get the content of the flag. What is the flag?
	- We can find the secret.js file by using the Browser DevTools and navigating to the Debugger tab.
	- We can then see the code within the file, where we are able to find the file:
	- HTB{1_4m_7h3_53r14l_g3n3r470r!}