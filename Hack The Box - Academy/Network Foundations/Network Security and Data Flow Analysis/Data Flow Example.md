# Accessing a Website - The Process
- **Connect to Wi-Fi**
    - Laptop finds the correct SSID.
    - User authenticates with a WPA2/WPA3 password.
    - DHCP begins network configuration.
- **Obtain Network Settings (DHCP)**
    - Laptop requests an IP address if it doesn't already have one.
    - Router's DHCP server assigns:
        - Private IP address (e.g., 192.168.1.10)
        - Subnet mask
        - Default gateway
        - DNS server
- **Resolve Domain Name (DNS)**
    - Laptop sends a DNS query for **[www.example.com](http://www.example.com)**.
    - DNS server returns the website's IP address (e.g., 93.184.216.34).
- **Encapsulation and Transmission**
    - **Application Layer:** Browser creates an HTTP/HTTPS request.
    - **Transport Layer:** Request is wrapped in a TCP segment (port 80 or 443).
    - **Internet Layer:** TCP segment is placed in an IP packet.
    - **Link Layer:** IP packet is placed in an Ethernet/Wi-Fi frame with MAC addresses.
    - Laptop uses **ARP** to find the router's MAC address and sends the frame.
- **Network Address Translation (NAT)**
    - Router replaces the laptop's private IP with its public IP.
    - Packet is forwarded through the ISP and across the internet.
- **Server Processing**
    - Server firewall checks the request.
    - Web server (Apache, Nginx, IIS, etc.) processes it.
    - Server sends webpage data (HTML, CSS, JavaScript, images) back.
- **Response and Decapsulation**
    - Router uses NAT to map the response back to the laptop's private IP.
    - Laptop removes frame, IP, and TCP headers.
    - Browser renders the webpage.



# Diagram
![[Pasted image 20260612014541.png]]