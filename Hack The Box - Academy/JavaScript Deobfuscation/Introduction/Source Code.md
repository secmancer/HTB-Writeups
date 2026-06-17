- Most websites use **JavaScript** to handle their functionality.
- **HTML** defines the website’s structure and elements.
- **CSS** determines the website’s visual design.
- **JavaScript** executes the functions that make the website interactive.
- These processes occur in the **background**, with users only seeing the front-end interface.
- Although all code runs on the **client-side**, browsers render it, so users rarely inspect it.
- To analyze a website’s **client-side behavior**, examining the **page source code** is the starting point.
- The section aims to explain how to **access and understand** this source code and its purpose.


# HTML
- Open Firefox in the PwnBox and visit the target URL: `http://SERVER_IP:PORT`.
- Page title: **Secret Serial Generator** — the page displays that text but has no visible input fields or obvious functionality.
- Next step: inspect the page source to find hidden/client-side logic.
- In Firefox press **Ctrl + U** to open the source view (`view-source:http://SERVER_IP:PORT`).
- The HTML source will show the page structure (title, elements) and any linked CSS (e.g., full-page width/height styles).
- Developers often leave **comments** or extra information in the HTML — these can reveal functionality or sensitive data.
- Reading comments and the source can help uncover client-side behavior and hidden strings, endpoints, or keys.
- Always examine the source when the UI shows no obvious inputs — useful first step in analyzing client-side features.


# CSS
- **CSS placement options:**
    - Defined **internally** within `<style>` tags inside the HTML file.
    - Defined **externally** in a separate `.css` file linked via `<link>` in the HTML `<head>`.
- **Current case:**
    - CSS is **internally defined** between `<style>` tags.
    - Example includes universal selectors (`*`, `html`) resetting margins, padding, and borders.
    - Sets specific font sizes for elements like `<h1>` and `<p>`.
- **External example:**
    - `<link rel="stylesheet" href="style.css">` inside the `<head>` section links an external CSS file.


# JavaScript
- What is code obfuscation?
	- Code obfuscation is intentionally transforming source code so it still runs the same but is **harder for humans to read and understand**.
	- Goal: hide logic, algorithms, secrets, or make reverse-engineering/time-based analysis more expensive.
- Common techniques (how it’s done)
	- **Minification / whitespace removal** — removes formatting and shortens names; easy to reverse with a prettifier.
	- **Identifier renaming** — replaces meaningful variable/function names with short meaningless names (`a`, `b`, `_0x12f`).
	- **String encoding/packing** — strings are stored encoded (hex/base64/rot/Unicode) and decoded at runtime.
	- **Eval/`Function`/dynamic code generation** — constructs code as strings and executes it, hiding original structure.
	- **Control-flow flattening / opaque predicates** — reorder and wrap code in confusing branches, loops, or always-true/false checks.
	- **Dead code / junk insertion** — add unreachable or irrelevant code to increase noise.
	- **Layered/wrapping (packers)** — multiple layers of encoding/decoding (e.g., `eval(unescape(...))`) requiring iterative unpacking.
	- **Virtualization / bytecode generation** — compile code into a custom VM bytecode and an interpreter in JS (very hard to reverse).
	- **Anti-debugging / tamper checks** — detect devtools or breakpoints and alter behavior.
- Where it’s used
	- **Commercial protection** — protect proprietary logic in client-side apps (e.g., licensing checks, commercial SDKs).
	- **Anti-cheat / anti-fraud** — hide game logic or detection mechanisms.
	- **Malware / malicious scripts** — to hide payloads and evade detection.
	- **CTF / obfuscated puzzles** — deliberately as a challenge.
	- **Ad trackers / analytics** — sometimes obfuscated to hinder analysis or block circumvention.
- Downsides / caveats
	- **Not a substitute for secure design** — secrets in client code can still be extracted; obfuscation only raises cost.
	- **Performance impact** — runtime decoding or big evals can slow things down.
	- **Hard to debug & maintain** — developers suffer without source maps.	    
	- **False sense of security** — determined analysts/tools can often recover logic.
- How to analyze / deobfuscate (practical steps)
	1. **Prettify / format** — use browser devtools or a JS beautifier to restore indentation.
	2. **Look for packers** — common patterns: `eval(function(p,a,c,k,e,d){...})`, `unescape`, `atob`, long hex arrays. These indicate layered packing.
	3. **Iteratively unpack** — replace `eval(...)` with `console.log(...)` or run in a sandboxed Node instance to get the intermediate decoded string, then prettify again.
	4. **Static tools** — use JS unpackers/deobfuscators, AST parsers (esprima, acorn) or dedicated tools (deobfuscator scripts, online unpackers).
	5. **Dynamic debugging** — set breakpoints before the eval, step through in DevTools, inspect variables/decoded strings.
	6. **Search for strings & endpoints** — once partially deobfuscated, look for URLs, keys, or hidden logic.
	7. **Recover identifier meaning** — rename short identifiers to meaningful names as you figure out their roles.
	8. **Use source maps if available** — sometimes `.map` files are present and map back to original code.
	9. **Automate with scripts** — write small Node scripts to repeatedly decode layers (use `vm` module or `eval` carefully in a sandbox).
	10. **Be careful & legal** — don’t run unknown code on your host; use isolated VMs or containers.
-  Quick checklist you can run on `secret.js`
	- Open in DevTools → Sources → click “Pretty print” ( `{ }` ).
	- Search for `eval(`, `Function(`, `unescape`, `atob`, hex arrays, or long base64 strings.
	- Replace outer `eval` with `console.log` (or intercept via breakpoint) to extract inner payload.
	- Repeat until you get readable code or strings you can analyze.


# Questions
- Repeat what we've done in this section, and you should find a secret flag, what is it?
	- We can open up the Browser DevTools and see the flag within the code from the Inspector tag
		-  HTB{4lw4y5_r34d_7h3_50urc3}