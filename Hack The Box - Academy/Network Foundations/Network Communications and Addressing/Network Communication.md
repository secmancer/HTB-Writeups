# **Core Components of Network Communication**  
- For any network to operate efficiently, three key elements—**MAC addresses**, **IP addresses**, and **ports**—work together to ensure data reaches the correct destination across local and global networks.


# **1. MAC Addresses**
- **Definition:**
	- **Media Access Control (MAC) address** — a **unique identifier** assigned to a device’s **Network Interface Card (NIC)**.
	- Operates at the **Data Link Layer (Layer 2)** of the OSI model.
	- Format: **48-bit hexadecimal**, e.g., `00:1A:2B:3C:4D:5E`.
	- Structure:
	    - First 24 bits → **Organizationally Unique Identifier (OUI)** (manufacturer).
	    - Last 24 bits → **Device-specific identifier**.
- **Purpose & Use:**
- Enables **device recognition within a local network (LAN)**.
- Used by **switches** to forward data frames to the correct device.
- **ARP (Address Resolution Protocol)** maps IP addresses to MAC addresses, linking logical and physical addressing.
- **Example:**
	- Computer A (IP: 192.168.1.2, MAC: 00:1A:2B:3C:4D:5E) sends data to Computer B (IP: 192.168.1.5, MAC: 00:1A:2B:3C:4D:5F).
	- Computer A uses **ARP** to find B’s MAC, encapsulates the frame, and the **switch** forwards it to the correct port.


### **2. IP Addresses**
- **Definition:**
	- An **Internet Protocol (IP) address** uniquely identifies a device on a network using the **Internet Protocol**.
	- Operates at the **Network Layer (Layer 3)** of the OSI model.
	- Used for **locating and routing** data across interconnected networks.
	- **Two versions:**
	    - **IPv4:** 32-bit (e.g., `192.168.1.1`).
	    - **IPv6:** 128-bit (e.g., `2001:0db8:85a3::8a2e:0370:7334`).
- **Purpose & Use:**
	- Enables communication **within and across different networks**.
	- **Routers** use IP addresses to determine the most efficient data path.
	- IP addresses are **logical** and can **change** depending on network configuration.


# **3. Ports**
- **Definition:**
	- A **numerical identifier** assigned to specific processes or network services.
	- Operates at the **Transport Layer (Layer 4)** of the OSI model.
	- Works with **TCP** (connection-oriented) and **UDP** (connectionless) protocols.
	- Allows multiple applications to share the same IP address while directing traffic to the right process.
- **How Ports Work:**
	- A **client application** initiates a connection using a **destination port**.
	- The **server** listens on that port (e.g., port 80 for HTTP).
	- The **operating system** directs traffic to the correct application based on port number.
- **Example:**
	- **HTTP** uses port **80** (unencrypted web).
	- **HTTPS** uses port **443** (secure web).
	- Port range: **0–65535**, divided into categories:
    

|Port Type|Range|Purpose|Example|
|---|---|---|---|
|**Well-Known**|0–1023|Common Internet services|HTTP (80), HTTPS (443), FTP (20–21)|
|**Registered**|1024–49151|Vendor/service-specific|SQL Server (1433)|
|**Dynamic/Private**|49152–65535|Temporary client sessions|Browser’s temporary port for web access|


# **Example: Browsing the Internet**
1. **DNS Lookup:**
    - Resolves domain name (e.g., _example.com_) to IP (e.g., `93.184.216.34`).
2. **Data Encapsulation:**
    - Browser generates HTTP request.
    - TCP encapsulates it, specifying **port 80/443**.
    - Packet includes destination **IP address**.
    - **ARP** finds MAC address of the router (default gateway).
3. **Data Transmission:**
    - Frame sent to router’s MAC.
    - Router forwards packet based on destination **IP**.
    - Intermediate routers continue routing toward the server.
4. **Server Processing:**
    - Server receives the packet on port **80/443**.
    - Processes the request and prepares a response.
5. **Response Transmission:**
    - Response sent back to client’s **ephemeral (temporary)** port.
    - Packet travels back through routers, guided by IP and port information, until it reaches the client.


# **Key Takeaways**
- **MAC Addresses:** Identify **physical devices** on a local network.
- **IP Addresses:** Identify **logical locations** across networks.
- **Ports:** Identify **specific applications/services** using those addresses.
- Together, they ensure **accurate, organized, and secure data transmission** throughout network communication.


# Questions
- What protocol maps IP addresses to MAC addresses?
	- ARP
- Which IP version uses 128-bit addressing?
	- IPv6
- At which layer of the OSI model do ports operate? (Format: two words)
	- transport layer
- What is the designated port number for HTTP?
	- 80
- What is the first step in the process of a web browsing session? (Format: two words)
	- DNS lookup