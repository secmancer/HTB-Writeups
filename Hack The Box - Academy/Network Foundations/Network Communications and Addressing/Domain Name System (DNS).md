# Domain Name
- Readable address that is easy to remember


# IP Address
- numerical label


# DNS Hierarchy
- Root Servers
- Top-Level Domains (TLDs)
- Second-level Domains
- Subdomains / Hostnames
![[Pasted image 20260612010923.png]]


# DNS Resolution PRocess
1) www.example.com is given
2) Local DNS cache checked first
3) If not found, queries recursive DNS server
4) Recursive DNS server contacts root server
5) Root server returns the TLD name server
6) TLD Name server gives the query to the authoritative name server for example.com
7) Authoritative name server responds with www.example.com's IP address
8) Recursive server returns the IP directly to the user to get them connected
![[Pasted image 20260612011109.png]]


# Questions
- ### What type of domain is `.com` considered as? (Format: Three words, example: One-Two Three)
	- Top-Level Domain
- ### In the domain `www.example.com`, what is `example` called?
	- second-level domain
- ### What is checked first in the DNS resolution process when you enter a domain name into a browser? (Format: Two words)
	- DNS cache
- ### What type of DNS server is typically provided by an Internet Service Provider?
	- recursive DNS server
- ### Which server directs the recursive DNS server to the appropriate TLD name server?
	- Root server
- ### What numerical label uniquely identifies a device on a network?
	- IP address
- ### In the URL "accounts.google.com", what is `accounts` considered as?
	- subdomain