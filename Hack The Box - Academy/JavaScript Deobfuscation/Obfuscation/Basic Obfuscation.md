- Code obfuscation is usually not done manually, as there are many tools for various languages that do automated code obfuscation. 
- Many online tools can be found to do so, though many malicious actors and professional developers develop their own obfuscation tools to make it more difficult to deobfuscate.


# Running JavaScript code
- **Example code:** `console.log('HTB JavaScript Deobfuscation Module');`
- **Purpose:** prints a message to the browser/JS console using `console.log()`.
- **Test environment used:** JSConsole (`https://jsconsole.com`) — paste the code and press Enter.
- **Observed output:** `HTB JavaScript Deobfuscation Module` appears in the console.
- **Why this matters:** confirms the cleartext behavior before obfuscation — a baseline to compare against after obfuscating the code.


# Minifying JavaScript code
- **JavaScript minification:** reduces code readability while keeping functionality intact.
- **Process:** compresses code into a single line by removing spaces, line breaks, and unnecessary characters.
- **Purpose:** more useful for longer scripts; a single-line script shows little difference when minified.
- **Tools:** online minifiers like [javascript-minifier.com](https://javascript-minifier.com).
- **Output testing:** running the minified code in JSConsole works the same as the original code.
- **File convention:** minified JS files usually use the `.min.js` extension.
- **Applicability:** minification is not limited to JavaScript — it can be used for other languages as well.


# Packing JavaScript code
- **Obfuscation example used:** transformed `console.log('HTB JavaScript Deobfuscation Module');` into a packed `eval(function(p,a,c,k,e,d){...})` form.
- **Tool shown:** BeautifyTools JavaScript obfuscator (packing technique).
- **Packed output:** uses a wrapper function with arguments `(p,a,c,k,e,d)` and a dictionary/lookup array (`'Module|Deobfuscation|JavaScript|HTB|log|console'.split('|')`).
- **Behavior preserved:** the obfuscated code still prints the same console message when executed (tested in JSConsole).
- **Packing principle:** the packer replaces original tokens with indexed references and reconstructs the original source at runtime.
- **Packer fingerprint:** the `(p,a,c,k,e,d)` wrapper and six-argument pattern commonly indicate a packer.
- **Visibility caveat:** some important strings (like literal messages) may remain in cleartext inside the packed payload, revealing behavior.
- **Limitation:** while packing reduces readability, sensitive data can still be exposed via remaining clear strings — more advanced obfuscation needed to hide those.