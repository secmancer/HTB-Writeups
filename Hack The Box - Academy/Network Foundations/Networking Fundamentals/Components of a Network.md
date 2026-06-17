# 1. Core Network Components

## Primary Categories
- End Devices:
    - computers, smartphones, tablets, IoT, Smart Devices
- Intermediary Devices:
    - Switches, Routers, Modems, Access Points
- Network Media:
    - Cables, Protocols
- Software Components:
    - Management/Firewall Software
- Servers:
    - Web Servers, File Servers, Mail Servers, Database Servers
---
# 2. End Devices (Hosts)
## Definition
- Device that sends or receives data within a connected network
## Role in Network
- Data generation
- Data consumption
- User interaction
- Interface to:
    - The World Wide Web
## Examples
- PCs, smart devices, etc
## Connection Types
- Wired:
    - Ethernet
- Wireless:
    - Wi-Fi
---
# 3. Intermediary Devices
## Definition
- facilitate how the flow of data between end devices
## Core Responsibilities
- Packet forwarding
- Path determination
- Traffic management
- Congestion prevention
- Security enforcement
## Operate at OSI Layers
- Routers: Network Layer
- Switches: Data Link Layer
## Security Features
- Firewalls
- Access control
- Traffic filtering
---
# 4. Network Interface Cards (NICs)
## Definition
- hardware component that allows for a connection to the network, often via Ethernet for wired or Wi-Fi for wireless
## Primary Functions
- Physical Ethernet interface
- Data transmission
- Data reception
## Addressing
- Unique identifier:
    - Media Access Control address (MAC)
- Operates at OSI Layer:
    - Data Link Layer
## Types
- Wired NIC:
	- Ethernet
- Wireless NIC:
	- Wi-Fi
---

# 5. Routers
## Definition
- intermediary device that forwards data packets between networks
## OSI Layer
- Network Layer
## Responsibilities
- Packet forwarding
- IP-based decision making
- Traffic management
- Path selection
- Network interconnection
## Routing Mechanisms
- Routing tables
- Routing protocols
    - OSPF
    - BGP
## Security Features
- Firewalls
- ACLs (Access Control Lists)
---
# 6. Switches
## Definition
- connect multiple devices within the same network, typically done with a LAN
## OSI Layer
- Data Link Layer
## Addressing Used
- MAC addresses
## Responsibilities
- Connect devices within
- Reduce congestion
- Improve performance
---
# 7. Hubs (Legacy Device)
## Definition
- connects multiple devices together and then sends out the data, like a switch, but does it without regard of the destination
## OSI Layer
- Physical Layer
## Why Inefficient
- Collisions
- Casual broadcast behavior
## Modern Replacement
- Switches
---
# 8. Network Media
## Wired Media
- Twisted Pair
- Coaxial
- Fiber Optic
## Wireless Media
- Wi-Fi
- Bluetooth
- Radio waves
- Microwaves
- Infrared
## Performance Factors
- Speed
- Reliability
- Distance limitations
---
# 9. Cabling and Connectors

## Purpose
- link devices onto the network
## Common Connectors
- RJ-45 plug
- Used to connect:
    - Devices that are capable of internet
## Impact on Network
- Performance
- Speed
- Reliability
---
# 10. Network Protocols
## Definition
- rules/conventions that control how data is formatted, transmitted, received, and interpreted
## Ensure
- Standardization
- Compatibility
- Data formatting
- Addressing
- Routing
- Error checking
- Synchronization
## Common Protocols
- TCP/IP
- HTTP/HTTPS
- FTP
- SMTP
---
# 11. Network Management Software

## Definition

## Core Functions

- Performance monitoring:
    
- Configuration management:
    
- Fault analysis:
    
- Security management:
    

## Used By

## Example Use Case

---

# 12. Software Firewalls (Host-Based Firewalls)

## Definition

## Difference from Hardware Firewall

## Functions

- Traffic monitoring:
    
- Rule enforcement:
    
- Block unauthorized access:
    
- Application-level control:
    

## Example

- IPTables:
    
- OS built-in firewall:
    

---

# 13. Servers

## Definition

## Client-Server Model

- Server role:
    
- Client role:
    

## Core Functions

- Service hosting:
    
- Resource sharing:
    
- Data management:
    
- Authentication:
    
- Permission management:
    

## Types of Servers

- Web Server:
    
- File Server:
    
- Mail Server:
    
- Database Server:
    

## Example (Website Access)

- Browser sends:
    
- Server processes:
    
- Server responds:
    

---

# 14. Big Picture Summary

## End Devices

## Intermediary Devices

## Servers

## Media & Protocols

## Together They Enable

---


# Questions
- ### What type of network cable is used to transmit data over long distances with minimal signal loss?
	- fiber-optic
- ### Which protocol manages data routing and delivery across networks?
	- TCP/IP
- ### What software is used to oversee and administer network operations? (Format: 3 words)
	- network management software
- ### What software is used to protect individual devices from unauthorized network access? (Format: 1 word)
	- firewall
- ### What type of cable is used to connect components within a local area network for high-speed data transfer?
	- ethernet
- ### Which device connects multiple networks and manages data traffic to optimize performance?
	- router