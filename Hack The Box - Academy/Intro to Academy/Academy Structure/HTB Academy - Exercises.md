# What is an Exercise?
- Most **interactive sections** conclude with **exercises** to reinforce learning.
- Exercises typically include a **Docker** or **VM target** to practice on.
- You can start a target by clicking **“Click here to spawn the target system!”**
- Once spawned, access details are displayed in the format `http://<ip>:<port>`.
- Some targets also provide **login credentials** (username and password) for access.

> **Note:** Only a single target per user can be active at any one time. Each target has a timer that shows how much time is left before it is terminated, but it can be manually extended or re-spawned by clicking on the appropriate buttons.


# Docker Targets
- Many exercises, particularly in **web modules**, use **Docker targets** for convenience and speed.
- Docker targets require **no additional setup** and are **quick to launch**.
- Once active, you can:
    - **Click the IP/PORT** to copy it.
    - **Access the target** directly (e.g., in a browser for web-based modules).
- Most Docker targets are ready immediately, though some may take up to a minute to initialize.

> **Note:** You can spot a docker target by its lack of a VPN button, as no VPN connection is required to access it.


# VM Targets
- Some modules require **advanced targets**, such as:
    - **Windows**, **Active Directory (AD)**, or **network environment** systems.
- These modules use **Virtual Machine (VM) targets** instead of Docker containers.
- VM targets start similarly to Docker targets but may take longer to initialize.
- You can access the VM:
    - Directly from your **Workstation (PwnBox)** once the IP appears, or        
    - From your **own machine** by connecting with the **VPN key**, downloadable via the **Download VPN Connection File** button.

> **Note:** To find out more about connecting to the HTB Academy VPN, check out [this help article](https://help.hackthebox.com/en/articles/9297532-connecting-to-academy-vpn).


# Completing an Exercise
- Some questions include a **Hint** button to guide you if you're stuck.
- Enter your **answer or flag** in the field and click **Submit** to complete the question.
- Correct answers reward you with **cubes**, which can be used to unlock other modules.
- Most questions are **required** to complete a section.
- **Optional Exercises** can be skipped or solved by clicking **Reveal Answer**, allowing section completion without solving them.

> **Note:** You can always use the exercise targets to practice what was shown in the section. However, solving the exercise will not always match the exact commands shown in the section, as they will have some variance to test your understanding and gradually build your skills. Exercises in easier modules will have a minor variance from the shown demo, while harder modules will be more challenging.


# Questions
- ### Start the above target, copy the shown IP:PORT by clicking on them, and then paste them in your browser. What's the proof shown in the page?
	- t4rg3ts