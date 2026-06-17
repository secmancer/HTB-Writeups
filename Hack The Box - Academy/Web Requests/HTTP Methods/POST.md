- **POST requests** are used when web applications need to send data or files from the client to the server.
- Unlike **GET**, which appends parameters to the URL, **POST** places them in the **HTTP request body**.
- **Advantages of POST:**
    - **Lack of Logging:** Large data (like file uploads) isn’t stored in URLs or logs, reducing clutter and exposure.
    - **Less Encoding Requirements:** Data in the body can include binary content and doesn’t need URL-safe encoding.
    - **More Data Capacity:** URLs have length limits (~2,000 characters), while POST bodies can handle much larger payloads.
- **Common uses:** file uploads, form submissions, API data transfers.
- Tools like **cURL** or browser **DevTools** can capture and send POST requests for inspection or testing.


# Login Forms
- The web application uses a **PHP login form** instead of HTTP Basic Authentication.
- Logging in with **admin:admin** grants access and reveals a search function.
- Using browser **DevTools → Network tab**, filtering by the server IP shows a **POST request** containing credentials.
- Viewing the **Request → Raw** tab displays the sent data:
    ```bash
    username=admin&password=admin
    ```    
- This confirms the credentials are sent in the **HTTP request body**.
- To replicate the request with **cURL**, use:
    ```bash
    curl -X POST -d 'username=admin&password=admin' http://<SERVER_IP>:<PORT>/
    ```
- The returned HTML includes the search page instead of the login form — indicating **successful authentication**.
- **Tip:** Many login forms redirect after login (e.g., `/dashboard.php`). Use **`-L`** with `curl` to automatically **follow redirects**.


# Authenticated Cookies
- After successful login, the server returns a **Set-Cookie** header containing a **session cookie** (e.g., `PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1`).
- This cookie allows **persistent authentication**, so credentials don’t need to be re-entered for each request.
- Use **`-v`** or **`-i`** with `curl` to view the response headers and confirm cookie receipt.
- To reuse the cookie, send it with `curl` using:
    ```bash
    curl -b 'PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1' http://<SERVER_IP>:<PORT>/
    ```
- Alternatively, set it manually as a header:
    ```bash
    curl -H 'Cookie: PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1' http://<SERVER_IP>:<PORT>/
    ```
- Both methods authenticate successfully without resending credentials.
- In **browser DevTools**, cookies can be viewed and edited in the **Storage tab (Shift + F9)**.
    - Replace or add a cookie manually (name = `PHPSESSID`, value = session token).
    - Refreshing the page with a valid cookie grants access without logging in.    
- Having a **valid session cookie** is often enough for authentication — a key concept in many **web attacks**, including **Cross-Site Scripting (XSS)** and **session hijacking**.


# JSON Data
- Using **browser DevTools → Network tab**, clearing requests, and performing a search (e.g., “London”) shows a **POST request** to `/search.php`.
- The request body contains JSON data:
    ```json
    {"search":"london"}
    ```
- The request includes the header `Content-Type: application/json`, indicating the payload format.
- Full request headers show additional information like `Host`, `User-Agent`, `Referer`, and a valid session cookie (`PHPSESSID`).
- The same request can be replicated with **cURL**:
    ```bash
    curl -X POST -d '{"search":"london"}' \
    -b 'PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1' \
    -H 'Content-Type: application/json' \
    http://<SERVER_IP>:<PORT>/search.php
    ```
- The response returns `["London (UK)"]`, confirming the query succeeded and authentication persisted through the cookie.
- Omitting the **cookie** or **Content-Type** header causes the request to fail or return an error (e.g., unauthenticated or invalid data).
- The same request can be executed in the **browser console** using **Fetch API**:
    ```javascript
    fetch('http://<SERVER_IP>:<PORT>/search.php', {
      method: 'POST',
      headers: {'Content-Type': 'application/json'},
      credentials: 'include',
      body: JSON.stringify({search: 'london'})
    }).then(res => res.json()).then(console.log)
    ```
- This demonstrates how to interact directly with backend endpoints — a useful technique in **web app testing** and **bug bounty** work for analyzing API behavior and bypassing the UI.


# Questions
- Obtain a session cookie through a valid login, and then use the cookie with cURL to search for the flag through a JSON POST request to '/search.php'
	- Like before, visiting the website and logging in while having the tools up allows us to capture the session cookie
	- Cookie: PHPSESSID=**rdi27bqe3o8urf48mhfcqchkl7**
	- We can then use it to send a POST request searching for the flag:
	- curl -X POST -d '{"search":"flag"}' -b 'PHPSESSID=rdi27bqe3o8urf48mhfcqchkl7' -H 'Content-Type: application/json' http://83.136.250.87:55377/search.php
	- Flag: HTB{p0$t_r3p34t3r}