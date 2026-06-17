- **Every InfoSec domain** faces its own unique **risks and threats**, influenced by:
    - The **domain’s purpose and scope**.   
    - The **technologies and systems** it uses.
    - The **type and sensitivity** of data it handles.
    - The **vulnerabilities** in its design and operation.
- **Distributed Denial of Service (DDoS) Attack:**
    - A **malicious attempt** to disrupt a website, server, or online service by flooding it with **massive internet traffic**.
    - Differs from a **DoS attack**, which comes from **one source**; a **DDoS** uses **multiple compromised devices** (a **botnet**)
    - **Goal:** Overwhelm system resources so **legitimate users** can’t access the service.
- **Analogy — The Bakery Example:**
    - You host a bakery’s grand opening, but a **huge disruptive crowd** floods the shop.      
    - Real customers can’t enter, even though the bakery itself isn’t broken.
    - In a DDoS, the **botnet (crowd)** floods your **server (bakery)** with fake traffic, blocking legitimate requests.        
    - The **attackers** are like the orchestrators sending the crowd to cause chaos and shut you down temporarily.


# How it works
- A **DDoS attack** consists of **three main components:**
    1. **The Attacker:** The individual or group that coordinates the attack to disrupt a specific target.
    2. **The Botnet (Amplification Network):** A collection of **compromised devices**—computers, servers, and IoT devices—controlled remotely without their owners’ knowledge.
    3. **The Victim:** The **targeted server, service, or network** that the attacker intends to incapacitate.
- **How it works:**
    - The attacker sends commands to the botnet, instructing all infected devices to **flood the target** with requests simultaneously.
    - This **overwhelms bandwidth and processing resources**, causing severe slowdowns or complete crashes.
    - As a result, **legitimate users** experience service delays or outages.
- **Analogy — The Small Shop Scenario:**
    - A **massive crowd (botnet)** is ordered to rush into a **small shop (victim)**.
    - The **overcrowding** prevents employees from moving or working effectively.
    - Operations grind to a halt, mirroring how a DDoS attack **paralyzes** an online service through excessive, coordinated traffic.


# Impact
- **2016 Dyn DDoS Attack:**
    - Targeted **Dyn**, a major DNS and internet service provider.
    - Impacted over **50 major websites** including **Twitter, Netflix, and Reddit**, causing widespread outages in the U.S. and Europe.
    - Attackers used the **Mirai botnet**, which hijacked **IoT devices** like home routers and security cameras.
    - Demonstrated how **everyday connected devices** can be exploited to launch **large-scale, global attacks**.
- **Consequences of DDoS Attacks:**
    - **Financial Impact:**
        - Significant **loss of revenue** from downtime, especially for **e-commerce, banking, and streaming services**.
    - **Reputational Damage:**
        - Repeated or extended outages **erode customer trust** and push users toward competitors.
    - **Operational Disruptions:**
        - Interrupt essential online services, affecting both **businesses and end users** who rely on them.
    - **Diversion Tactic:**
        - DDoS attacks can act as a **smokescreen** for deeper intrusions, such as **data breaches or malware installation**, while defenders focus on restoring availability.
- **Key Takeaway:**
    - The Dyn incident underscored the **global reach and cascading impact** of modern DDoS attacks, proving that even **consumer-grade IoT devices** can be weaponized to disrupt critical online infrastructure.