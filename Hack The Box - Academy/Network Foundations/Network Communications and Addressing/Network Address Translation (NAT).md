# Public vs Private IP Addresses
- Public: unique identifiers, assigned by ISPs
- Private: used in local networks, not routable to the global internet.

# How do we translate between the two?
- NAT (Network Address Translation)
- Translates private IP addresses to a single public IP address, usually assigned to the router


# How NAT Works
- NAT keeps track of IP mappings
- Usually on the router, the router will take the private IP address, and then edit the src IP filed from that IP to its own IP.
- That way, when it is then forwarded from the router, it will look like it is coming from the router only
![[Pasted image 20260612005940.png]]


# NAT Types
- Static: one-to-one mapping
- Dynamic: public IP picked from a IP address pool, done so based on the demand
- Port Address Translation (PAT): common NAT in home networks, multiple private IPs share one single public IP


# Benefits vs Tradeoffs
- Benefits
	- Conserves limited space
	- Basic layer of security added
	- Flexibility
- Tradeoffs
	- Hard to implement in more complex situations
	- Breaks certain protocols that need end-to-end connectivity
	- Adds complexity overall


# Questions
- ### What type of NAT allows multiple private IP addresses to share one public IP address using unique port numbers?
	- Port Address Translation
- ### What RFC specifies private IP ranges?
	- RFC 1918
- ### Which NAT type involves a one-to-one mapping of private IP addresses to public IP addresses?
	- Static NAT
- ### What type of NAT assigns a public IP from a pool as needed?
	- Dynamic NAT
- ### What device typically performs NAT in a home network?
	- Router