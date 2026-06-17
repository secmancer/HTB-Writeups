- HTTP transfers all data in clear text, making it vulnerable to Man-in-the-Middle (MiTM) attacks.
- Attackers can intercept and view unencrypted HTTP data.
- HTTPS (HTTP Secure) was developed to encrypt communications, protecting data from interception.
- Encrypted HTTPS traffic prevents third parties from extracting transmitted information.
- HTTPS is now the standard for websites, while HTTP is being phased out.
- Most modern browsers are discontinuing support for non-secure HTTP sites.


# Overview
- HTTP requests transmit data in plain text, exposing sensitive information like usernames and passwords.
- Example: An HTTP POST request to `/login.php` can be intercepted, revealing credentials in clear text.
- Attackers on the same network (e.g., public Wi-Fi) can easily capture and reuse such credentials.
- HTTPS encrypts all transmitted data, shown in Wireshark as TLS-encrypted streams over port 443.
- Encrypted HTTPS traffic prevents interception and exposure of sensitive information.
- HTTPS websites are identified by “https://” in the URL and a lock icon in the browser’s address bar.
- Example: Visiting `https://www.google.com` ensures all traffic is encrypted.
- However, HTTPS may still leak the visited domain if using a clear-text DNS server. 
- To prevent DNS leaks, use encrypted DNS (e.g., 8.8.8.8 or 1.1.1.1) or a VPN to secure all traffic.


# HTTPS Flow
![[Pasted image 20251023174346.png]]
- Typing `http://` to a site that enforces HTTPS starts with an unencrypted request to port 80.
- The server responds with a `301 Moved Permanently` redirect to the `https://` URL (port 443).
- The client then begins the TLS handshake: the browser sends a **Client Hello** (supported protocols/ciphers).
- The server replies with a **Server Hello** and its SSL/TLS certificate; key exchange information follows.
- The client validates the server certificate and performs its part of the key exchange.
- An encrypted handshake completes to confirm symmetric keys and negotiation parameters.
- After the handshake succeeds, normal HTTP requests/responses continue — but now all application data is encrypted by TLS.
- The high-level key-exchange details (cryptographic math, certificate chain verification) are beyond this module’s scope.
- Attackers can attempt an HTTP downgrade (MiTM) to force clear-text HTTP, but modern browsers/servers implement protections against this.


# cURL for HTTPS
- `curl` automatically handles HTTPS: it performs the TLS handshake and encrypts/decrypts data for you.
- If the server’s SSL certificate is invalid or the chain is broken, `curl` will refuse the connection by default to prevent MiTM attacks.
- Example `curl` error: `curl: (60) SSL certificate problem: Invalid certificate chain`.
- Modern browsers behave the same — they warn/block sites with invalid certificates.
- Development or practice sites often use invalid/self-signed/outdated certs and can trigger this error.
- To bypass certificate validation with `curl` (insecure), use `-k` / `--insecure`: `curl -k https://example.com`.
- `-k` lets the request proceed and returns the response, but it defeats certificate-based security and exposes you to MiTM risk.
- Safer alternatives to `-k`: install the site’s CA into your trust store, use `--cacert` with a specific CA file, or create a trusted dev certificate (e.g., `mkcert`) or run the service on localhost.
- Use `-k` only for controlled testing environments — never for sensitive production connections.