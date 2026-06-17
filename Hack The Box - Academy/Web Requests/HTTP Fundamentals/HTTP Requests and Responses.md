- HTTP communication is composed of two parts: an **HTTP request** and an **HTTP response**.
- The **client** (e.g., browser or `curl`) sends the HTTP request to the **server** (e.g., web server).
- The request includes details such as the **resource URL/path**, **parameters**, **headers**, and any **data** being sent.
- The **server** processes the request and sends back an **HTTP response**.
- The response contains a **status code** and may include the requested **resource/data** if access is allowed.


# HTTP Request
![[Pasted image 20251023174645.png]]
- Example request: `GET /users/login.html HTTP/1.1` to `http://inlanefreight.com/users/login.html`.
- The **first line** of an HTTP request has three fields separated by spaces:
    - **Method:** specifies the action (e.g., `GET`).
    - **Path:** the resource being accessed (e.g., `/users/login.html`, possibly with a query string).
    - **Version:** the HTTP version (e.g., `HTTP/1.1`).
- Following lines are **HTTP headers**, given as key–value pairs (e.g., `Host`, `User-Agent`, `Cookie`).
- Headers define various attributes of the request and end with a **blank line** indicating their completion.
- The request may include a **body**, usually for methods like `POST` or `PUT`.
- **HTTP/1.x** transmits data as clear-text with newline delimiters.
- **HTTP/2.x** uses a binary, dictionary-based format for efficiency and security.


# HTTP Response
![[Pasted image 20251023174706.png]]


# cURL
- - `curl` can show the **full HTTP request and response** when run with the `-v` (verbose) flag.
- Example behavior shown by `curl -v inlanefreight.com`: connection attempts and TCP info are printed first (`Trying SERVER_IP:80...`, `Connected to ...`).
- Lines beginning with `>` are the **request** sent by the client (e.g. `> GET / HTTP/1.1`, `> Host: inlanefreight.com`, `> User-Agent: curl/7.65.3`).
- Lines beginning with `<` are the **response** from the server (e.g. `< HTTP/1.1 401 Unauthorized`, response headers like `Date`, `Content-Length`, `Content-Type`).
- The response body (HTML, JSON, etc.) is printed after the response headers — the same body that `curl` returns without `-v`.
- `HTTP/1.1 401 Unauthorized` in the example indicates the client is not authorized to access the resource.
- `-vvv` increases verbosity further (shows additional low-level details such as extra protocol/debug info and more handshake/connection details).
- Use `-v` (or `-vvv`) when testing or doing web pentests to inspect raw requests, headers, status codes, and server responses.


# Browser DevTools
- Most modern web browsers come with built-in developer tools (`DevTools`), which are mainly intended for developers to test their web applications. However, as web penetration testers, these tools can be a vital asset in any web assessment we perform, as a browser (and its DevTools) are among the assets we are most likely to have in every web assessment exercise. In this module, we will also discuss how to utilize some of the basic browser devtools to assess and monitor different types of web requests.
- Whenever we visit any website or access any web application, our browser sends multiple web requests and handles multiple HTTP responses to render the final view we see in the browser window. To open the browser devtools in either Chrome or Firefox, we can click `CTRL+SHIFT+I` or simply click `F12`. The devtools contain multiple tabs, each of which has its own use. We will mostly be focusing on the `Network` tab in this module, as it is responsible for web requests.
- If we click on the Network tab and refresh the page, we should be able to see the list of requests sent by the page: ![Network tab showing two GET requests to 188.166.146.97:31122. Status 304 for '/' and 404 for 'favicon.ico'.](https://academy.hackthebox.com/storage/modules/35/devtools_network_requests.jpg)
- As we can see, the devtools show us at a glance the response status (i.e. response code), the request method used (`GET`), the requested resource (i.e. URL/domain), along with the requested path. Furthermore, we can use `Filter URLs` to search for a specific request, in case the website loads too many to go through.


# Questions
- What is the HTTP method used while intercepting the request?
	- GET
- Send a GET request to the above server, and read the response headers to find the version of Apache running on the server, then submit it as the answer. (answer format: X.Y.ZZ)
	- We can do this by running: **curl http://94.237.61.88:36716 -vv**
	- 2.4.41