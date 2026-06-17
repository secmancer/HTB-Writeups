# 1. Networking in the Modern Technology Stack
## TCP/IP Stack Importance
- Modern technology built on: TCP/IP
## Topics Covered in This Section
- OSI Model
- TCP/IP Model
- Common Network Protocols
- Transmission methods
---
# 2. OSI Model (Open Systems Interconnection)
## Purpose
- Conceptual framework for:
	- telecommunication and computing systems
- Standardizes:
	- functionality on these systems
- Why interoperability matters:
	- vendors/developers can create devices/software that can work with each other    
## 7 Layers of OSI Model
### Layer 1 – Physical
- Primary function:
	- Transmit raw bitstreams over a physical medium
- Responsible for:
    - Physical connection between devices
- Hardware examples:
    - Ethernet cables, hubs, repeaters
---
### Layer 2 – Data Link
- Primary function:
	- Node-to-node data transferring
- Node-to-node transfer means:
    - Direct link between two physically connected nodes
- Error handling responsibilities:
    - Error detection/correction, along with proper synchronization
- Devices operating here:
    - Switches, bridges
- Addressing type used:
    - MAC (Media Access Control)
---
### Layer 3 – Network
- Primary function:
	- packet forwarding, which entails routing them through different routers to ensure they reach the destination network
- Responsible for:
    - logical addressing and path determination
- Logical addressing:
    - ensure data reaches the correct destination as a packet travels through many networks
- Devices operating here:
    - routers
- Protocol used:
    - IP (Internet Protocol)
---
### Layer 4 – Transport
- Primary function:
	- Provide end-to-end communication services for applications
- Services provided:
	- Ensurance for delivery of data
    - Segmentation
    - Reassembly of messages
    - Flow control
    - Error checking
- Protocols:
    - TCP (Transmission Control Protocol)
	    - Reliable, connection-oriented communication with guaranteed delivery
    - UDP (User Datagram Protocol)
	    - faster, connectionless communication without guaranteed delivery
---
### Layer 5 – Session
- Manages:
    - sessions between applications
- Session responsibilities:
	 - Establish, maintain, and terminate connections 
- Essential for checkpointing/recovery
	- Ensures data transfer can resume seamlessly after any interruption
- Role of protocols/APIs at this layer
	- Operate to coordinate communication between the systems and their applications
---
### Layer 6 – Presentation
- Role:
	- Translator between the application layer and network format
- Handles:
    - Data representation
    - Encryption/Decryption
    - Compression
    - Format conversion
---
### Layer 7 – Application
- Provides:
	- Network services directly to end-user applications
- Features
	- Resource sharing
	- Remote file access
	- Other similar network services
- Common protocols:
    - HTTP (Hypertext Transfer Protocol)
	    - web browsing
    - FTP (File Transfer Protocol)
        - file transfers
    - SMTP (Simple Mail Transfer Protocol)
        - email transmission
    - DNS (Domain Name System)
	    - resolving domain names to their IP addresses
---
# 4. TCP/IP Model
## Purpose
- Condensed version of the OSI model
- Practical implementation focus:
	- Internet and network
## 4 Layers of TCP/IP Model
---
### 1. Link Layer (Network Interface)
- Corresponds to OSI layers:
    - Physical and Data Link layers
- Responsibilities:
    - Handle physical aspects of network hardware/media
- Technologies:
	- Ethernet, Wi-Fi
---
### 2. Internet Layer
- Responsible for:
    - Logical addressing of devices and routing packets across networks
- Logical addressing:
    - Uses IP
- Routing:
    - Ensures data reaches its intended destination by finding logical paths for transmit it through
- Protocols:
    - IP (Internet Protocol)
    - ICMP (Internet Control Message Protocol)
- Corresponds to OSI layer:
	- Network Layer
---
### 3. Transport Layer
- Provides:
	- End-to-end communication services that are essential for the functioning of the Internet.
- Protocols:
    - TCP
    - UDP
- Corresponds to OSI layer:
	- Transport Layer
---
### 4. Application Layer
- Contains:
	- Specific data communication services to applications
- Example protocols:
    - HTTP
    - FTP
    - SMTP
- Corresponds to OSI layers:
	- Session, Presentation, Application
---
# 5. OSI vs TCP/IP Comparison
## OSI Model
- Number of layers: 7
- Nature: Practical application
- Primary use: Protocols being used on the Internet
## TCP/IP Model
- Number of layers: 4
- Nature: More application focus
- Primary use: Internet-based data exchange
---
# 8. Protocols
## Definition
- Protocols are:
	- Standardized rules that determine the formatting/processing of data to facilitate communication between devices in a network
- Examples
	- HTTP
	- FTP
	- SMTP
	- TCP
	- UDP
	- IP
---

# 9. Common Network Protocols

## Application Layer Protocols

### HTTP
- Primarily used for transferring web pages. It operates at the Application Layer, allowing browsers and servers to communicate in the delivery of web content.
### FTP
- Facilitates the transfer of files between systems, also functioning at the Application Layer. It provides a way for users to upload or download files to and from servers.
### SMTP
- Handles the transmission of email. Operating at the Application Layer, it is responsible for sending messages from one server to another, ensuring they reach their intended recipients.
---
## Transport Layer Protocols
### TCP
- Ensures reliable data transmission through error checking and recovery, operating at the Transport Layer. It establishes a connection between sender and receiver to guarantee the delivery of data in the correct order.
### UDP
- Allows for fast, connectionless communication, which operates without error recovery. This makes it ideal for applications that require speed over reliability, such as streaming services. UDP operates at the Transport Layer.
---
## Internet Layer Protocol

### IP
- Crucial for routing packets across network boundaries, functioning at the Internet Layer. It handles the addressing and routing of packets to ensure they travel from the source to the destination across diverse networks.    
---
# 10. Transmission
## Definition
- Transmission refers to:
	- Process of sending data signals over a medium from one device to another\
---
# 11. Transmission Types
## Analog
- Signal type: continuous
- Example: traditional radio broadcasts
## Digital
- Signal type: discrete
- Used in: computer networks and digital telephony
---
# 12. Transmission Modes
## Simplex
- Direction: One-way
- Example:
	- Keyboard to computer
## Half-Duplex
- Direction: Two-way, but must go one at a time
- Example:
	- Walkie-talkies
## Full-Duplex
- Direction: Full two-way
- Example:
	- Telephone calls
---
# 13. Transmission Media

## Wired Media

### Twisted Pair
- Used in: Ethernet, LAN
### Coaxial Cable
- Used in: cable TV, early Ethernet
### Fiber Optic
- Signal type: light pulses
- Used for: High speed internet
---
## Wireless Media

### Radio Waves
- Used for: Wi-Fi, cellular networks
### Microwaves
- Used for: satellite communications
### Infrared
- Used for: short-range communications (remote control)
---


# Questions
- ### What layer of the OSI model is responsible for physical connections like Ethernet cables? (Format: two words)
	- physical layer
- ### Name the OSI layer that deals with logical addressing and routing. (Format: two words)
	- network layer
- ### Which protocol ensures reliable delivery of data and operates at the Transport Layer?
	- TCP
- ### At what layer do switches operate within the OSI model? (Format: three words)
	- data link layer
- ### What layer of the TCP/IP model corresponds to the OSI model’s Application, Presentation, and Session layers? (Format: two words)
	- application layer
- ### Which layer of the OSI model manages data encryption and data format conversion? (Format: two words)
	- presentation layer
- ### Name a protocol used for web browsing that operates at the Application Layer.
	- HTTP
- ### Which OSI layer ensures the segments are transferred reliably and in sequence? (Format: two words)
	- transport layer
- ### Which protocol provides fast, connectionless communication and operates at the Transport Layer?
	- UDP