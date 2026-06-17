# **Introduction to DHCP (Dynamic Host Configuration Protocol)**
- **Purpose:**
    - Automates the assignment of **IP addresses** and network configurations to devices.
    - Eliminates manual configuration, reducing errors and administrative work.
    - Ensures each device receives a **unique IP address**, avoiding conflicts.
    - Recycles unused IP addresses when devices disconnect (efficient address pool use).


# **How DHCP Works – The DORA Process**
- **DORA** = **Discover → Offer → Request → Acknowledge**

| Step               | Description                                                              |
| ------------------ | ------------------------------------------------------------------------ |
| **1. Discover**    | Client broadcasts a **DHCP Discover** message to find available servers. |
| **2. Offer**       | DHCP server responds with a **DHCP Offer**, proposing an IP lease.       |
| **3. Request**     | Client sends a **DHCP Request** message, accepting the offered IP.       |
| **4. Acknowledge** | Server replies with a **DHCP Acknowledge**, confirming the assignment.   |

- **Roles:**
	- **DHCP Server:** Manages the pool of IPs and configuration details (subnet mask, gateway, DNS).
	- **DHCP Client:** Any device that requests network configuration automatically.


# **Lease Time and Renewal**
- IP assignments are **temporary** (known as a **lease**).
- Example: A DHCP server assigns IP `192.168.1.10` for **24 hours**.
- Before expiry, the client sends a **renewal request** to extend the lease.
- The DHCP server responds with an **Acknowledge**, renewing the lease if available.


# **Example Scenario**
- Alice connects her **new laptop** to the office network.
- **Discover:** Laptop sends a broadcast to find DHCP servers.
- **Offer:** Server proposes IP address `192.168.1.10`.
- **Request:** Laptop accepts the offer.
- **Acknowledge:** Server confirms the assignment.
- The laptop now communicates on the network using `192.168.1.10`.
- When the lease nears expiration, the laptop sends a **renewal request** to continue using the same IP.


# **Key Takeaways**
- **DHCP automates IP management**, reducing manual setup and configuration errors.
- Ensures **unique IP allocation** and prevents address duplication.
- Uses the **DORA process** to dynamically assign and confirm IP addresses.
- **Leases are temporary** and must be **renewed periodically**.
- Common in both **home** and **enterprise networks**, supporting scalability and efficient management.


# Questions
- What protocol automates IP address configuration for devices on a network?
	- DHCP
- What acronym describes the sequence of messages exchanged during the DHCP process?
	- DORA
- What type of message does a client send to accept an IP address from a DHCP server?
	- request