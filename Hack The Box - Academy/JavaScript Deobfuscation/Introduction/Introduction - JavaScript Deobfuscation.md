# What you’ll learn (quick)
- find where JS lives inside HTML (inline, `<script src=…>`, event handlers, data-attributes)
- common obfuscation techniques (minification, string/hex/Unicode encoding, control-flow flattening, `eval`, self-defending code)
- step-by-step deobfuscation tactics (beautify, symbol recovery, replace evals, decode strings)
- decoding encoded payloads (Base64, hex, percent-encoding, custom maps)
- basic static/dynamic analysis (read code, run it safely, add logging/breakpoints)
- send basic HTTP requests from deobf’d code (fetch/XHR/curl) to see what it calls


# Tools & environment (must-have)
- modern browser DevTools (Network, Sources, Console, Breakpoints)
- Node.js (run snippets safely) — `node script.js`
- Code formatter / beautifier (Prettier, js-beautify)
- A sandbox VM or isolated container — **do not run unknown code on your main machine**
- Optional online helpers: JS deobfuscators / string decoders (only in sandboxed environments)
- Familiarity with regexp and basic JS (variables, functions, async/promises)


# Practical, safe workflow (step-by-step)
1. **Isolate** — put the page/code into an offline sandbox or VM.
2. **Locate** scripts: search HTML for `<script>` tags and event attributes. Save files locally.
3. **Beautify** the JS so you can read it (preserve original for reference).
4. **Search for telltale patterns**: `eval(`, `Function(`, `atob(`, long arrays of strings, `replace`/`join`/index lookups.
5. **Statically simplify**: replace obfuscated name collisions with readable names, collapse trivial expressions, remove dead code.
6. **Extract string tables**: when you see arrays like `['a','b','c']` used by indexers, reconstruct the mapping.
7. **Safely execute dynamic parts**:
    - prefer to run _small_ snippets in Node/REPL with console logging instead of full `eval`.
    - wrap suspicious `eval` payloads to `console.log()` the argument first.
8. **Instrument**: put `console.log` or breakpoints to see runtime values, network calls, decoded strings.
9. **Decode** encodings: Base64 (`atob`/`Buffer.from(...,'base64')`), hex, URL-encoded, or custom substitution tables.
10. **Document** each transformation — keep original + each deobfuscation step so you can reproduce results.


# Common quick commands/snippets
- Run JS in Node and print result:
    ```bash
    node -e "console.log(require('./script').someExportedFn())"
    ```
- Base64 decode in Node:
    ```js
    Buffer.from('c29tZSBiYXNlNjQ=', 'base64').toString()
    ```
- Beautify file (with js-beautify installed via npm):
    ```bash
    npx js-beautify script.js -r
    ```


# Typical tricks you’ll encounter
- string arrays + index lookup (replace with direct strings)
- nested `eval` / `Function` wrappers (unwrap stepwise)
- char-code math (e.g. `String.fromCharCode(x+1)`) — compute to reveal strings
- control-flow obfuscation (jump tables) — inline and simplify
- anti-tamper checks (prevent execution if code changed) — run in a controlled environment and neutralize checks by editing guard conditions


# Safety & ethics
- **Never** execute unknown, untrusted JS on your host. Use a VM or ephemeral container.
- Don’t reveal or request CTF/flag solutions from me; I’ll help with methods and tooling but not with direct flag retrieval. (You already saw I’ll refuse that.)
- If code attempts network calls, block external access while analyzing or route through a controlled proxy to inspect traffic.


# Ready-made exercises (try these)
- find a small obfuscated snippet and: beautify → replace string table → log output
- take an encoded `eval(atob('...'))` and decode it stepwise, documenting each output
- intercept a script’s network call in DevTools, replay it with `fetch` from Console
	- If you want, I can:
	- give you a **short obfuscated snippet** now and walk you through deobfuscating it step-by-step, or   
	- provide a **checklist** you can copy into your sandbox before you start analyzing real samples.