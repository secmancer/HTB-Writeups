# CIA Triad
- Confidentiality: only authorized users can view the data
- Integrity:  the data remains accurate and unaltered
- Availability: network resources are accessible when needed


# Firewalls
- A **firewall** is a hardware or software security device that monitors and controls incoming and outgoing network traffic based on predefined rules.
- It acts like a **security guard**, allowing authorized traffic and blocking unauthorized traffic.
- Firewalls filter traffic using criteria such as:
    - IP addresses
    - Port numbers
    - Protocols
- They can also **log events** and **alert administrators** about suspicious activity.


# Types of Firewalls
- **Packet Filtering Firewall**
    - Operates at OSI Layers 3 and 4.
    - Filters traffic based on IP addresses, ports, and protocols.
    - Example: Allowing only HTTP (80) and HTTPS (443).
- **Stateful Inspection Firewall**
    - Tracks active network connections.
    - Only allows traffic that belongs to an established connection.
- **Application Layer (Proxy) Firewall**
    - Operates up to Layer 7.
    - Inspects application data and content.
    - Example: Blocking malicious HTTP requests.
- **Next-Generation Firewall (NGFW)**
    - Combines stateful inspection with advanced security features.
    - Includes deep packet inspection (DPI), intrusion detection/prevention (IDS/IPS), and application control.

![[Pasted image 20260612014140.png]]

# Firewall Placement
- **Home networks:** Firewall is usually built into the router/modem.
- **Business networks:** Firewall is often a dedicated device placed between the internet/router and the internal network so all traffic passes through it.


# pfSense
- **pfSense** is a popular open-source router/firewall platform with many add-on packages and advanced security features.


# Intrusion Detection and Prevention Systems (IDS/IPS)
- **IDS (Intrusion Detection System):**
    - Monitors network or system activity for suspicious behavior.
    - Generates alerts but does **not block** threats.
- **IPS (Intrusion Prevention System):**
    - Monitors activity like an IDS.
    - **Detects and blocks** malicious traffic in real time.
- Detection Methods
	- Signature-based detection
	- Anomaly-based detection
- Common placement
	- **Behind the firewall** to inspect traffic that passes firewall filtering.
	- **In a DMZ (Demilitarized Zone)** to protect public-facing servers.
	- **On endpoints** such as servers and workstations.
- ### Example Tool
	- **Suricata** is a popular open-source solution that can operate as both an IDS and an IPS.


# Types of IDS/IPS
- **Network-Based IDS/IPS (NIDS/NIPS)**
    - Monitors traffic across the network.
    - Typically placed at key network points.
    - Example: A sensor monitoring data center traffic.
- **Host-Based IDS/IPS (HIDS/HIPS)**
    - Runs on individual devices.
    - Monitors local traffic, logs, and system activity.
    - Example: Antivirus or endpoint security software.


# Security Best Practices
- **Define Clear Policies:** Follow the principle of least privilege.
- **Regular Updates:** Keep firewalls, IDS/IPS signatures, and systems updated.
- **Monitor Logs:** Review firewall logs and alerts regularly.
- **Layered Security:** Use defense in depth (firewalls, IDS/IPS, antivirus, endpoint protection).
- **Periodic Penetration Testing:** Simulate attacks to verify security effectiveness.


# Questions
- ### What device monitors network traffic and enforces rules to allow or block specific traffic?
	- firewall
- ### Which type of firewall operates at the network and transport layers of the OSI model? (Format: two words)
	- packet filtering
- ### What advanced feature does a Next-Generation Firewall include beyond stateful inspection? (Format: three words)
	- deep packet inspection
- ### Which system generates alerts for suspicious network activity without blocking it? (Format: acronym)
	- IDS
- ### Which system not only detects but also prevents suspicious network activity by blocking it? (Format: acronym)
	- IPS
- ### What detection method involves comparing network traffic against a database of known exploits? (Format: three words)
	- signature-based detection