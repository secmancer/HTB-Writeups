- **HTTP methods** define how a client interacts with a server resource.
- They instruct the server **how to process** the request and **how to respond**.
- Common examples include `GET`, `POST`, `PUT`, `DELETE`, etc.
- In `curl -v` output, the **first line** shows the method (e.g., `GET / HTTP/1.1`).
- In **browser devtools**, the **Method column** displays the HTTP method used.
- The **response headers** include the **HTTP status code**, indicating the outcome of the request.


# Request Methods
- **Common HTTP methods:**    
    - **GET:** Retrieves a specific resource; can include data via query strings (e.g., `?param=value`).        
    - **POST:** Sends data to the server in the request body; used for forms, logins, or file uploads.
    - **HEAD:** Returns only the headers of a GET request (no body); useful for checking resource info or size.
    - **PUT:** Creates or replaces a resource on the server; insecure use can allow malicious uploads.
    - **DELETE:** Removes a resource from the server; insecure use can cause DoS or data loss.
    - **OPTIONS:** Returns allowed HTTP methods and general server information.
    - **PATCH:** Performs partial updates to an existing resource.
- The **server and application configuration** determine which methods are allowed.
- **Modern web apps** primarily use **GET** and **POST**, while **REST APIs** also rely on **PUT** and **DELETE** for data modification and removal.


# Status Codes
- **HTTP status codes** indicate the **result** of a client’s request.
- They are grouped into **five main classes:**
    - **1xx – Informational:** Provides status info; doesn’t affect request processing.
    - **2xx – Success:** The request was successfully processed.
    - **3xx – Redirection:** The client is redirected to another resource or URL.
    - **4xx – Client Error:** The request is invalid or unauthorized.
    - **5xx – Server Error:** The server failed to process a valid request.
- **Common examples:**
    - **200 OK:** Successful request; response body contains the requested data.
    - **302 Found:** Redirects client to another URL (e.g., after login).
    - **400 Bad Request:** Malformed or invalid request syntax.
    - **403 Forbidden:** Access denied; user lacks permissions or sent malicious input.
    - **404 Not Found:** Requested resource does not exist.
    - **500 Internal Server Error:** Server encountered an error while processing the request.
- Some providers (e.g., **Cloudflare**, **AWS**) define **custom status codes** beyond standard HTTP ones.