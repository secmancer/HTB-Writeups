- In the previous section, we found out that the `secret.js` main function is sending an empty `POST` request to `/serial.php`. 
- In this section, we will attempt to do the same using `cURL` to send a `POST` request to `/serial.php`. 
- To learn more about `cURL` and web requests, you can check out the [Web Requests](https://academy.hackthebox.com/module/details/35) module.


# cURL
- **What cURL is:** command-line tool available on Linux, macOS, and modern PowerShell for making HTTP requests.
- **How it’s used:** provide a URL to fetch a resource and receive the response as plain text.
- **Example command:** `curl http://SERVER_IP:PORT/` (runs from the shell prompt `secmancer@htb[/htb]$`).
- **Returned output:** the server responded with the HTML for the “Secret Serial Generator” page (DOCTYPE, `<head>`, styles, and the page body).
- **Content note:** the HTML shown matches the source code you examined earlier — it’s the same page that generates secret serials.


# POST Request
- **Goal:** send an HTTP `POST` from the command line to replicate what the page / server does.
- **Use `-X POST` to set method:** `curl -X POST http://SERVER_IP:PORT/` forces a POST request.
- **`-d` to include POST data:** `-d "param1=sample"` adds form data in `application/x-www-form-urlencoded` format.
- **`-s` for quiet output:** `-s` (silent) hides progress and reduces clutter in the response.
- **Example full command:** `curl -s -X POST -d "param1=sample" http://SERVER_IP:PORT/`
- **Practical note:** `curl -d` implicitly uses `POST`, so `-X POST` is usually unnecessary when `-d` is present.
- **Multiple parameters:** include multiple `-d` flags or a single quoted string with `&` (e.g., `-d "a=1&b=2"`).    
- **Content-Type behavior:** by default `-d` sends `application/x-www-form-urlencoded`; to send JSON add `-H "Content-Type: application/json"` and pass a JSON payload.
- **Next step (your plan):** use the above to replicate the client behavior and test how `server.js` (or `/serial.php`) responds to POSTs.


# Questions
- Try applying what you learned in this section by sending a 'POST' request to '/serial.php'. What is the response you get?
	- Similar to what we did before:
		- curl -s http://83.136.249.47:35026/serial.php -X POST
	- We then get this string:
		- N2gxNV8xNV9hX3MzY3IzN19tMzU1NGcz