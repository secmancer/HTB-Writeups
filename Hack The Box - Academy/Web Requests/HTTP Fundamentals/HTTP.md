- **HTTP (HyperText Transfer Protocol):** an application-layer protocol used to request and transfer resources on the World Wide Web.
- **Hypertext:** text that contains links to other resources for easy navigation.
- **Client–Server Model:** the **client** (e.g., web browser or mobile app) sends an HTTP request to the **server**, which processes the request and returns the resource (HTTP response).
- **Default port:** HTTP typically uses **port 80** (configurable by the server).
- **URLs and FQDNs:** users access web resources by entering a **URL** that contains a **Fully Qualified Domain Name (FQDN)** (e.g., `www.hackthebox.com`) pointing to the desired server/resource.
- **Web and mobile apps:** most modern applications rely on HTTP(S) requests to communicate with backend services.


# URL
- Resources over HTTP are accessed via a `URL`, which offers many more specifications than simply specifying a website we want to visit. 
- Let's look at the structure of a URL:
![[Pasted image 20251023172612.png]]

| Component    | Example             | Description                                                                                                                                                                           |
| ------------ | ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Scheme       | http:// or https:// | This is used to identify the protocol being accessed by the client, and ends with a colon and a double slash (`://`)                                                                  |
| User Info    | admin:password@     | This is an optional component that contains the credentials (separated by a colon `:`) used to authenticate to the host, and is separated from the host with an at sign (`@`)         |
| Host         | inlanefreight.com   | The host signifies the resource location. This can be a hostname or an IP address                                                                                                     |
| Port         | :80                 | The `Port` is separated from the `Host` by a colon (`:`). If no port is specified, `http` schemes default to port `80` and `https` default to port `443`                              |
| Path         | /dashboard.php      | This points to the resource being accessed, which can be a file or a folder. If there is no path specified, the server returns the default index (e.g. `index.html`).                 |
| Query String | ?login=true         | The query string starts with a question mark (`?`), and consists of a parameter (e.g. `login`) and a value (e.g. `true`). Multiple parameters can be separated by an ampersand (`&`). |
| Fragments    | #status             | Fragments are processed by the browsers on the client-side to locate sections within the primary resource (e.g. a header or section on the page).                                     |
- Not all components are required to access a resource. The main mandatory fields are the scheme and the host, without which the request would have no resource to request.


# HTTP Flow
![[Pasted image 20251023172943.png]]
- **DNS Resolution:**
    - When a user enters a URL (e.g., `inlanefreight.com`) in their browser, the browser first queries a **DNS server** to translate the **domain name** into its corresponding **IP address**.
    - The **DNS server** returns the IP, allowing communication with the correct web server.
- **Local DNS Check:**
    - The browser first checks the **`/etc/hosts`** file for a record.
    - If the domain isn’t found locally, it then queries external DNS servers.
    - You can manually add mappings in `/etc/hosts` using the format:
        ```
        <IP address>  <domain name>
        ```     
- **HTTP Request Process:**
    1. After obtaining the IP, the browser sends a **GET request** to the server (usually on **port 80**) for the root path `/`.
    2. The **web server** receives the request, processes it, and returns the **index file** (commonly `index.html`).
    3. The response includes an **HTTP status code** (e.g., `200 OK`), indicating success.
    4. The **browser renders** the returned HTML content for the user to view.
- **Key Concept:**
    - This process outlines the **basic anatomy of an HTTP request and response**, where the **client requests** a resource and the **server responds** accordingly.
- **Note:**
    - This explanation focuses on HTTP web requests. For deeper exploration of **HTML and web applications**, refer to the _Introduction to Web Applications_ module.


# cURL
- **Tools covered:** Web browser (Chrome/Firefox) and **cURL** (command-line tool/library for HTTP and many other protocols).
- **Why cURL:** Ideal for scripted/automated web requests and fast inspection of request/response context (prints raw HTML, does not render).
- **Basic usage:**
    - `curl inlanefreight.com` — send a simple GET request and print the raw response to stdout.
- **Download to file:**
    - `curl -O inlanefreight.com/index.html` — save using the remote filename.
    - `curl -o myfile.html inlanefreight.com/index.html` — save using a chosen filename.
    - `-s` (silent) suppresses progress/status output (e.g., `curl -s -O ...`).
- **Useful flags (examples):**
    - `-i, --include` — include response headers in output.
    - `-d, --data` — send HTTP POST data.
    - `-u, --user user:password` — provide basic auth credentials.
    - `-A, --user-agent` — set a custom User-Agent string.
    - `-v, --verbose` — verbose output for debugging.
- **Help & docs:**
    - `curl -h` — short help/overview.
    - `curl --help all` or `--help <category>` — full/detailed help.
    - `man curl` — read the manual page for complete documentation.
- **Notes for web penetration testing:**
    - cURL is faster and more convenient than a browser for examining raw requests/responses, scripting complex requests, and automating tests.
    - Use it to inspect headers, send custom payloads, emulate clients, and download resources for offline analysis.


# Questions
- To get the flag, start the above exercise, then use cURL to download the file returned by '/download.php' in the server shown above.
	- We just need to run: **curl 94.237.17.1:43032/download.php**
	- Flag: HTB{64$!c_cURL_u$3r}