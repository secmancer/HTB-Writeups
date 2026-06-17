- **HTTP headers** carry information between the **client** and **server** during communication.
- Some headers are specific to **requests** or **responses**, while others are **common to both**.
- Headers are written as **key–value pairs**, separated by a colon (`Header-Name: value`).
- Headers can contain **multiple values**, separated by commas or repeated lines.
- They are categorized into five main types:
    - **General Headers** – apply to both requests and responses (e.g., `Date`, `Connection`).
    - **Entity Headers** – describe the body’s content (e.g., `Content-Type`, `Content-Length`).
    - **Request Headers** – sent by the client to provide context (e.g., `Host`, `User-Agent`, `Accept`).
    - **Response Headers** – sent by the server to describe the response (e.g., `Server`, `Set-Cookie`).
    - **Security Headers** – used to enforce security policies (e.g., `Strict-Transport-Security`, `Content-Security-Policy`).


# General Headers
- **General headers** appear in both HTTP **requests** and **responses** and describe the **message itself**, not its content.
- Common examples:
    - **Date:** `Date: Wed, 16 Feb 2022 10:38:44 GMT`
        - Indicates when the message was created or sent.
        - Typically uses **UTC** time format.
    - **Connection:** `Connection: close` or `Connection: keep-alive`
        - Controls whether the connection remains open after the request.
        - `close` → terminate the connection after completion.
        - `keep-alive` → keep the connection open for additional requests or data.


# Entity Headers
- **Entity headers** describe the **content (entity)** carried by an HTTP message.
- They can appear in both **requests** (e.g., POST, PUT) and **responses**, but are more common in responses.
- Common examples:
    - **Content-Type:** `Content-Type: text/html; charset=UTF-8`
        - Specifies the media type and character encoding of the content.
    - **Media-Type:** `Media-Type: application/pdf`
        - Similar to `Content-Type`; defines the data format being transferred.
    - **Boundary:** `boundary="b4e4fbd93540"`
        - Used to separate multiple content parts in a message (e.g., multipart form data).
    - **Content-Length:** `Content-Length: 385`
        - Indicates the size (in bytes) of the message body; used by the server to read data properly.
    - **Content-Encoding:** `Content-Encoding: gzip`
        - Specifies any encoding or compression (e.g., gzip, deflate) applied to the data before transmission.


# Request Headers
- **Request headers** are sent by the **client** and describe the **context of the request**, not the message content.
- Common examples:
    - **Host:** `Host: www.inlanefreight.com`
        - Specifies the target domain or IP for the request.
        - Important for virtual hosting and host enumeration in pentesting.
    - **User-Agent:** `User-Agent: curl/7.77.0`
        - Identifies the client software (browser, tool, OS).
        - Useful for fingerprinting or debugging client requests.
    - **Referer:** `Referer: http://www.inlanefreight.com/`
        - Shows the origin page of the request.
        - Can be manipulated, so it should not be fully trusted.
    - **Accept:** `Accept: */*`
        - Lists acceptable content types the client can handle (e.g., `text/html`, `application/json`).
    - **Cookie:** `Cookie: PHPSESSID=b4e4fbd93540`
        - Sends stored cookie data to maintain sessions or user preferences.
        - Multiple cookies are separated by semicolons.
    - **Authorization:** `Authorization: BASIC cGFzc3dvcmQK`
        - Provides credentials or tokens for client authentication.
        - Supports various schemes (Basic, Bearer, etc.), depending on the web server/application.


# Response Headers
- **Response headers** appear only in **HTTP responses** and provide **metadata about the response**, not the content itself.
- Common examples:
    - **Server:** `Server: Apache/2.2.14 (Win32)`
        - Identifies the web server software and version handling the request.
        - Useful for server fingerprinting or enumeration.
    - **Set-Cookie:** `Set-Cookie: PHPSESSID=b4e4fbd93540`
        - Sends cookies from the server to the client for session tracking or authentication.
        - Browsers store these cookies and include them in future requests.
    - **WWW-Authenticate:** `WWW-Authenticate: BASIC realm="localhost"`
        - Informs the client about the authentication method required to access the resource (e.g., Basic, Digest, Bearer).


# Security Headers
- **Security headers** are HTTP **response headers** that enforce **browser security policies** and protect against common web attacks.
- Common examples:
    - **Content-Security-Policy:** `Content-Security-Policy: script-src 'self'`
        - Restricts where resources (like scripts) can be loaded from.
        - Helps prevent **Cross-Site Scripting (XSS)** and code injection attacks.
    - **Strict-Transport-Security:** `Strict-Transport-Security: max-age=31536000`
        - Forces browsers to use **HTTPS** instead of HTTP.
        - Prevents data interception and protocol downgrade attacks.
    - **Referrer-Policy:** `Referrer-Policy: origin`
        - Controls how much referrer information is sent in requests.
        - Helps protect sensitive URLs and user data.
- Many more security headers exist, and **applications can define custom headers** as needed.
- Full lists of standard HTTP and security headers are available in official documentation.


# cURL
- The **`-v` flag** in `curl` shows both the **full HTTP request and response** details.
- The **`-I` flag** sends a **HEAD request**, displaying **only the response headers** (no body).
- The **`-i` flag** shows **both headers and body** for any type of request made.
- Example: `curl -I https://www.inlanefreight.com`
    - Displays server response headers such as `Date`, `Server`, `Content-Type`, `Set-Cookie`, `WWW-Authenticate`, and several **security headers** (`Content-Security-Policy`, `Strict-Transport-Security`, `Referrer-Policy`).
- **Exercises:**
    - Review each header and recall its purpose (from previous sections).
- **Setting headers manually:**
    - Use `-H` to specify a custom header (e.g., `-H "Host: example.com"`).
    - Use `-A` to change the **User-Agent** (e.g., `curl -A "Mozilla/5.0" https://www.inlanefreight.com`).
- You can confirm header changes using the **`-I`** or **`-v`** flags.


# Browser DevTools
- Browser **Developer Tools** can display **HTTP headers** for all network activity.
- Open the **Network tab** to see each request made by the page (e.g., `GET /`, `GET /favicon.ico`).
- Click on a request to view details such as **status codes** (e.g., `304`, `404`) and **headers**.
- The **Headers tab** shows both the **HTTP request** and **response headers**, organized by category.
- Clicking **Raw** displays the headers in their original, unformatted form.
- The **Cookies tab** lists any cookies associated with the request or response.
- This provides a quick, visual way to inspect and analyze HTTP communication directly in the browser.


# Questions
- The server above loads the flag after the page is loaded. Use the Network tab in the browser devtools to see what requests are made by the page, and find the request to the flag.
	- When we open up the Browser DevTools, we can see the packets sent over through the Network tab.
	- However, if we open it after the page loads, then we actually don't see the flag packet come there.
	- Therefore, if we do this, then we can reload the website to get the flag packet that we need (it's labeled with flag_*random characters*)
	- The actual flag text is able to be found in the Response Payload minitab.
	- Flag: HTB{p493_r3qu3$t$_m0n!t0r}