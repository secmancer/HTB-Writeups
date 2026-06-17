- Whenever we visit any URL, our browsers default to a GET request to obtain the remote resources hosted at that URL. 
- Once the browser receives the initial page it is requesting; it may send other requests using various HTTP methods.
- This can be observed through the Network tab in the browser devtools, as seen in the previous section.


# HTTP Basic Auth
- **Basic HTTP Authentication** is handled directly by the web server (not the web app) to protect specific pages or directories.
- The browser prompts for **username** and **password** before granting access.
- Example credentials: `admin:admin` → grant access to the protected page.
- Using `curl` without credentials returns:
    - `HTTP/1.1 401 Authorization Required`
    - Response header: `WWW-Authenticate: Basic realm="Access denied"` — confirms Basic Auth is required.
- To authenticate via `curl`:
    - Use the **`-u` flag**:
        ```bash
        curl -u admin:admin http://<SERVER_IP>:<PORT>/
        ```
        → Successfully retrieves the page.
    - Alternatively, include credentials in the URL:
        ```bash
        curl http://admin:admin@<SERVER_IP>:<PORT>/
        ```
- The same authentication method works in a browser when visiting the URL with embedded credentials.


# HTTP Authorization Header
- Using `curl -v` with Basic Auth shows the **encoded credentials** in the **Authorization header**.
- Example:
    - `Authorization: Basic YWRtaW46YWRtaW4=` → Base64 encoding of `admin:admin`.
- In modern authentication schemes (e.g., **JWT**), the header would appear as:
    - `Authorization: Bearer <token>`.
- You can **manually set headers** with `-H`, including multiple headers if needed:
    ```bash
    curl -H 'Authorization: Basic YWRtaW46YWRtaW4=' http://<SERVER_IP>:<PORT>/
    ```
    → Grants access, same as using `-u` or credentials in the URL.
- This demonstrates that Basic Auth simply encodes credentials, offering **no encryption or real security**.
- **Modern web applications** typically use **login forms** handled by backend code (e.g., PHP) that authenticate via **POST requests** and issue **cookies or tokens** to maintain sessions.


# GET Parameters
- Once authenticated, the page provides a **City Search** feature that queries a backend resource for matching results.
- Using **browser devtools → Network tab (CTRL+SHIFT+E)** lets you monitor outgoing HTTP requests.
- Clear previous requests with the **trash icon** before performing a new search.
- Entering a search term (e.g., “le”) triggers a **GET request** to `search.php?search=le` on `127.0.0.1`.
- The backend returns the results (e.g., “Leeds (UK)” and “Leicester (UK)”).
- You can replicate this request with `curl`:
    ```bash
    curl 'http://<SERVER_IP>:<PORT>/search.php?search=le' -H 'Authorization: Basic YWRtaW46YWRtaW4='
    ```
    → Produces the same output without the webpage layout.
- **Browser devtools** can export requests easily:
    - **Copy → Copy as cURL** to get a ready-to-run `curl` command.
    - **Copy → Copy as Fetch** to generate a JavaScript `fetch()` command.
- The `fetch()` command can be executed in the **Console tab (CTRL+SHIFT+K)** to send the same request and view the response directly.
- Only essential headers (like `Authorization`) are needed when reproducing the request manually.


# Questions
- The exercise above seems to be broken, as it returns incorrect results. Use the browser devtools to see what is the request it is sending when we search, and use cURL to search for 'flag' and obtain the flag.
	- When we login into the website, we assume the admin role. 
	- This means when we search for a city while viewing the Network tab in the Browsers DevTools, we are able to get easy authentication: 
		- 'Authorization: Basic YWRtaW46YWRtaW4='
	- Therefore, we can redo the search request with cURL, but use the authorization cookie to get the flag:
		- curl -X GET http://94.237.120.235:31861/search.php\?search\=flag -H 'Authorization: Basic YWRtaW46YWRtaW4='
	- Flag: HTB{curl_g3773r}