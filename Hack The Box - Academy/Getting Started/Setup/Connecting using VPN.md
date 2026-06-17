- A **Virtual Private Network (VPN)** enables secure access to a private/internal network over public networks.
- It allows users to **connect remotely** and interact with hosts and resources as if locally connected.
- VPNs create a **secure, encrypted communication channel**, protecting data from **eavesdropping** or unauthorized access.
- Common use case: employees connecting securely to a **corporate network** from remote locations.

![[Pasted image 20251026193945.png]]

- A **VPN** routes your internet traffic through a **private VPN server** instead of your ISP, masking your real IP address.
- Data appears to originate from the **VPN server’s public IP**, providing anonymity and security.
- **Two main types of remote access VPNs:**
    - **SSL VPN:**
        - Uses a **web browser** as the client.
        - Connects to an **SSL VPN gateway**.
        - Can grant access to **web-based apps** (e.g., email, intranet) or the **entire internal network**.
        - No need for specialized software installation.
    - **Client-based VPN:**
        - Requires dedicated **client software**.
        - Once connected, the device behaves as if it’s **on the corporate network**.
        - Access level depends on **server configuration** — full internal access or limited to a **remote worker segment**.


# Why Use A VPN?
- **Commercial VPN services** (e.g., NordVPN, Private Internet Access) let users connect to servers in different regions to **obscure browsing traffic** and **mask public IP addresses**.
- They offer **some privacy and security**, especially on **untrusted networks** (e.g., public Wi-Fi).
- **Risks:** providers may **log data**, **misrepresent security practices**, or **fail to protect user privacy**.
- **VPNs do not guarantee anonymity** or complete privacy — trust in the provider is essential.
- Useful for **bypassing network/firewall restrictions** or protecting against **hostile networks**, not for illicit activity.
- **Never rely on VPNs** to conceal or justify **nefarious or illegal actions**.


# Connecting to HTB VPN
- HTB and similar labs require connecting to the private lab network via a VPN; hosts inside the lab cannot reach the public internet.
- Treat the lab network as **hostile** — always connect from an isolated VM, not your primary/client assessment VM.
- Security best-practices when connected to lab VPNs:
    - Use a dedicated attack VM.
    - Disable password SSH auth on the attacking VM.
    - Lock down any services (web servers, file shares) on your attack VM.
    - Don’t leave client-sensitive data on the attack VM.
- Launch the VPN with OpenVPN:
    - `sudo openvpn user.ovpn` — `user.ovpn` is the downloaded VPN config/key.
    - Successful connection is indicated by: **`Initialization Sequence Completed`**.
- Verify the VPN network interface:
    - `ifconfig` — look for a `tun0` adapter with an internal lab IP (e.g., `inet 10.10.x.2`).
- Inspect routing to see which networks are reachable via the VPN:
    - `netstat -rn` — routes will show lab subnets (example: `10.10.14.0/23` via `tun0`, and `10.129.0.0/16` reachable through the VPN).
- Use the VPN only for authorized lab/assessment activity; don’t rely on it for anonymity or to conceal improper behavior.


# Help with VPN
- If this is your first time using a VPN, the following resources on the Hack The Box support portal will be helpful:
	- [Introduction to Lab Access](https://help.hackthebox.com/en/articles/5185687-gs-introduction-to-lab-access)
	- [Connection Troubleshooting](https://help.hackthebox.com/en/articles/5185536-t-connection-troubleshooting)
