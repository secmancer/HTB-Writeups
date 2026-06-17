- **Organization and documentation** are critical in all infosec activities — client assessments, CTFs, Academy modules, or HTB labs.
- Maintaining **clear, accurate, and detailed notes** from the start improves workflow, consistency, and efficiency.
- Strong documentation habits are valuable across **all infosec roles** and even in **other professional fields**.


# Folder Structure
- Keep a clear folder structure on your attack machine for every engagement (scoping, enumeration, exploitation evidence, creds, screenshots, logs, tools).
- Example project layout (one client, separate assessments):
    - `Projects/Acme Company/EPT/` → `evidence/` (credentials, data, screenshots), `logs/`, `scans/`, `scope/`, `tools/`
    - `Projects/Acme Company/IPT/` → same subfolders as EPT.
- Use `scope/` to store target lists (IPs, domains) you feed scanning tools.
- Store raw scan output and logs in `scans/` and `logs/` so findings are reproducible and auditable.
- Put proof artifacts (screenshots, exploit output, harvested data, credentials) in `evidence/` and keep them organized (subfolders per artifact type or per host).
- Personal preferences: some people create a folder per target host; others keep screenshots inside notes — pick the approach that fits your workflow.
- Experiment and settle on a structure that keeps you efficient and makes reporting simpler.
- Protect sensitive evidence (credentials, PII) — restrict permissions and consider encryption for stored artifacts.


# Note Taking Tools
- **Organization and productivity** are critical — even strong technical skills can’t compensate for poor organization.
- Choose a **note-taking tool** that fits your workflow; popular options include:
    - **Cherrytree**
    - **Visual Studio Code**
    - **Evernote**
    - **Notion**
    - **GitBook**
    - **Sublime Text**
    - **Notepad++**
- Tools like **Notion** and **GitBook** support advanced organization (wikis, cheat sheets, etc.).
- When working with **client data**, ensure it’s **stored locally only** — never synced to the cloud.
- **Tip:** Learn **Markdown** — it’s simple, widely supported, and great for creating clean, organized notes.


# Other Tools and Tips
- Maintain a **personal knowledge base** (choose a tool that fits your workflow).
- Include **quick reference guides** for common setup tasks and **cheat sheets** for commands used in each assessment phase.
- Aggregate every useful artifact from hands-on work: **payloads, commands, tips, notes** from boxes, labs, assessments, and courses.
- Keep content **searchable and well-organized** so you can quickly reuse snippets during engagements.
- Store **checklists** and **report templates** for different assessment types to speed up and standardize reporting.
- Build a **findings/vulnerability database** (spreadsheet or DB) containing: title, description, impact, remediation, and references.
- Maintain reusable **remediation/advice text** so report writing requires minimal customization.
- Regularly **review and prune** the knowledge base—remove outdated items and consolidate duplicates.
- Protect sensitive entries (credentials, client data) by **storing locally or encrypting** and never syncing them to cloud services for real engagements.
- Export or back up essential cheat sheets (each HTB Academy module provides downloadable cheat sheets) for offline reference.


# Moving On
- Experiment with different **note-taking tools** and create a **folder structure** that fits your workflow.
- Build organizational habits **early** to make consistent documentation second nature.
- Use the **Nibbles walkthrough** later in the module to **practice documenting** your process.
- Add the **commands from this module** to your personal **common commands cheat sheet** for future reference.