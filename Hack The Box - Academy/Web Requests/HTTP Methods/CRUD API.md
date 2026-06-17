- We saw examples of a `City Search` web application that uses PHP parameters to search for a city name in the previous sections. 
- This section will look at how such a web application may utilize APIs to perform the same thing, and we will directly interact with the API endpoint.


# APIs
- **APIs** (Application Programming Interfaces) allow clients to interact programmatically with web applications or databases.
- Many APIs map **HTTP methods** to **database operations** (CRUD model):
    - **GET** → Read data
    - **POST** → Create new data
    - **PUT** → Update existing data
    - **DELETE** → Remove data
- Example: updating a record in the `city` table where the city name is “london”:
    ```bash
    curl -X PUT http://<SERVER_IP>:<PORT>/api.php/city/london
    ```
- Here, the **endpoint path** (`/city/london`) identifies the target resource, while the **HTTP method** (`PUT`) defines the intended action (update).
- Additional data (like new field values) would typically be passed in the **request body** as JSON or form data.


# CRUD
- APIs allow performing specific operations on database entities using **HTTP methods**.
- The four main API operations (CRUD) are:
    - **Create → POST:** Adds new data to a database table.
    - **Read → GET:** Retrieves data from a database table.
    - **Update → PUT:** Modifies existing data in a database table.
    - **Delete → DELETE:** Removes a specific record from a database table.
- These operations form the foundation of **CRUD** and **RESTful APIs**.
- Different APIs may vary in structure and authentication methods.
- **Access control** determines which users can perform which operations or view specific results.
- For more detail on API design and functionality, refer to the _Introduction to Web Applications_ module.


# Read
- To **read data** from an API, specify the **endpoint**, table, and (optionally) a search term in the URL.
    ```bash
    curl http://<SERVER_IP>:<PORT>/api.php/city/london
    ```
- The response is returned in **JSON** format, e.g.:
    ```json
    [{"city_name":"London","country_name":"(UK)"}]
    ```
- To make the output more readable, pipe it through **jq** and suppress extra output with `-s`:
    ```bash
    curl -s http://<SERVER_IP>:<PORT>/api.php/city/london | jq
    ```
- You can search for partial matches (e.g., `/city/le`) to return all related results.
- Providing an **empty search term** (e.g., `/city/`) retrieves **all records** from the table.
- Visiting the same URLs in a **web browser** displays the JSON output directly in the page.


# Create
- To **create a new entry**, send a **POST request** with JSON data and the appropriate **Content-Type header**:
    ```bash
    curl -X POST http://<SERVER_IP>:<PORT>/api.php/city/ \
    -d '{"city_name":"HTB_City", "country_name":"HTB"}' \
    -H 'Content-Type: application/json'
    ```
- This adds a new record to the `city` table.
- To verify creation, perform a **GET request** for the new entry:
    ```bash
    curl -s http://<SERVER_IP>:<PORT>/api.php/city/HTB_City | jq
    ```
- The output confirms successful creation:
    ```json
    [
      {
        "city_name": "HTB_City",
        "country_name": "HTB"
      }
    ]
    ```
- **Exercise:** Use **browser DevTools → Console** to send a **Fetch POST** request replicating the same operation and confirm that the new city is added.


# Update
- **PUT** is used to **update** or **replace** existing API entries, while **DELETE** removes them.
- **PATCH** can also update entries but only modifies **specific fields** instead of the entire record.
- Use **OPTIONS** to check which methods (PUT, PATCH, etc.) the server supports.
- **Example PUT request:**
    ```bash
    curl -X PUT http://<SERVER_IP>:<PORT>/api.php/city/london \
    -d '{"city_name":"New_HTB_City", "country_name":"HTB"}' \
    -H 'Content-Type: application/json'
    ```
- This replaces the `london` record with a new entry named `New_HTB_City`.
- Verification:
    ```bash
    curl -s http://<SERVER_IP>:<PORT>/api.php/city/london | jq
    curl -s http://<SERVER_IP>:<PORT>/api.php/city/New_HTB_City | jq
    ```
- The second command confirms successful update:
    ```json
    [
      {
        "city_name": "New_HTB_City",
        "country_name": "HTB"
      }
    ]
    ```
- **Note:** Some APIs allow PUT to create new entries if they don’t exist, while others only update existing ones.
- **Exercise:** Try updating a **non-existent city** to test how the API handles such requests.


# Delete
- **DELETE** requests remove specific API entries.
- To delete a record, specify the resource and use the **DELETE method**:
    ```bash
    curl -X DELETE http://<SERVER_IP>:<PORT>/api.php/city/New_HTB_City
    ```
- Verifying deletion:
    ```bash
    curl -s http://<SERVER_IP>:<PORT>/api.php/city/New_HTB_City | jq
    ```
    - Returns `[]`, confirming the entry no longer exists.
- **Exercise:** Delete one of the cities you added earlier via POST and verify it’s removed by listing all entries.
- With this, all **CRUD operations** (Create, Read, Update, Delete) can be performed using `curl`.
- In real applications, these operations are **restricted by permissions** — users may only modify or delete their own data.
- **Authentication** is typically enforced using **cookies** or **authorization headers** (e.g., JWT tokens) before allowing write operations.


# Questions
- First, try to update any city's name to be 'flag'. Then, delete any city. Once done, search for a city named 'flag' to get the flag.
	- Update the city entry for London:
		- curl -X PUT http://94.237.48.35:39295/api.php/city/london -d '{"city_name":"flag"}' -H 'Content-Type: application/json'
	- Delete that city:
		- curl -X DELETE http://94.237.48.35:39295/api.php/city/Denver
	- Search for the city named 'flag':
		- curl -s http://94.237.48.35:39295/api.php/city/flag | jq
	- That will give us the flag:
```
[  
 {  
   "city_name": "flag",  
   "country_name": "HTB{crud_4p!_m4n!pul4t0r}"  
 }  
]
```
