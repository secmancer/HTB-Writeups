# Peer-to-Peer (P2P)
- Each device is its own client/server
- They can communicate with each other without a central server or have a partially centralized setup
![[Pasted image 20260612011632.png]]
- Advantages
	- Scalability
	- Resilience
	- Cost distrubution
- Disadvantages
	- Management complexity
	- Potential reliability issues
	- Security challenges


# Client-Server
- Clients all need to connect to a centralized server to communicate with other clients.
- Most widely used architecture across the Internet
![[Pasted image 20260612011743.png]]
- Two different tiers:
	- Single tier: client, server, and database all reside on the same machine
	- Two-tier: client and server is split from each other, database is usually still grouped with the server
	- Three-tier: client, server, and database are fully split from each other
	- N-Tier: used in way more complex systems that call for more servers
- Advantages
	- Centralized control
	- Security
	- Performance
- Disadvantages
	- Single point of failure
	- High cost and maintenance
	- Network congestion


# Hybrid Architecture
- A blend of both P2P and the Client-Server model
![[Pasted image 20260612012002.png]]
- Advantages
	- Efficiency
	- Control
- Disadvantages
	- Complex implementation
	- Potential single point of failure


# Cloud Architecture
- Infrastructure that is mostly hosted/managed by third-party computing providers
![[Pasted image 20260612012116.png]]
- Advantages
	- Scalability
	- Reduced cost and maintenance
	- Flexibility
- Disadvantages
	- Vendor lock-in
	- Security and compliance
	- Connectivity


# Software-Defined Architecture (SDN)
- Centralized control plane with a software-based controller
![[Pasted image 20260612012236.png]]
- Advantages
	- Centralized control
	- Programmable and automation
	- Scalability and efficiency
- Disadvantages
	- Controller vulnerability
	- Complex implementation


# Questions
- ### What type of architecture allows nodes to act as both client and server?
	- peer-to-peer
- ### What architecture combines elements of both Client-Server and Peer-to-Peer models?
	- hybrid
- ### Which cloud service model involves accessing applications over the internet without managing the underlying infrastructure?
	- SaaS
- ### In which architecture is the control plane separated from the data plane? (Format: two words, one of which is hyphenated)
	- software-defined networking
- ### Which architecture is known for decentralized data sharing without a central server?
	- peer-to-peer
- ### What model is used by video conferencing apps to combine centralized coordination with peer-to-peer data transfer?
	- hybrid