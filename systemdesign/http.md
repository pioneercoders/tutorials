#### 🌐 HTTP Protocol

**✅ What is HTTP?**

**HTTP (HyperText Transfer Protocol)** is the **foundation of data communication** on the **World Wide Web**. It defines how messages are formatted and transmitted, and how web servers and browsers should respond to various commands.


**📦 Key Characteristics**

- **Protocol Type**: Application Layer (works on top of TCP/IP)
- **Stateless**: Each request is independent and does not retain user data.
- **Text-Based**: Messages are human-readable and plain text.
- **Request-Response Model**: Communication happens between a **client** (like a browser) and a **server**.


**🔄 Basic Workflow**

1. **Client sends a request** to the server (e.g., ask for a web page).
2. **Server processes** the request.
3. **Server sends back a response**, usually HTML, JSON, etc.
4. **Client displays or processes** the response.


**🧾 HTTP Request Structure (from Client to Server)**

- **Method**: `GET`, `POST`, `PUT`, `DELETE`, etc.
- **URL**: The resource being requested.
- **Headers**: Extra information like browser type, language, etc.
- **Body**: (optional) Used with methods like `POST` and `PUT` to send data.


**📩 HTTP Response Structure (from Server to Client)**

- **Status Code**: Indicates the result (`200 OK`, `404 Not Found`, etc.)
- **Headers**: Info about server, content type, cache rules, etc.
- **Body**: The actual content (HTML page, JSON data, etc.)


**📘 Common HTTP Methods**

| Method | Description              |
|--------|--------------------------|
| GET    | Request data             |
| POST   | Submit data              |
| PUT    | Update existing data     |
| DELETE | Delete data              |


**📊 Common HTTP Status Codes**

| Code | Meaning              |
|------|----------------------|
| 200  | OK                   |
| 404  | Not Found            |
| 500  | Internal Server Error|
| 301  | Moved Permanently    |
| 401  | Unauthorized         |


**🔒 Secure Version**

- **HTTPS** = HTTP + SSL/TLS encryption
- Ensures **secure, encrypted communication** between client and server.


**🌍 Real-Life Example**

1. You open your browser and type: `https://example.com`
2. Browser sends a `GET` request to the server.
3. Server responds with HTML content.
4. Browser renders the web page.


**🧠 Summary**

- **HTTP** is the backbone of web communication.
- It enables browsers and servers to **talk**.
- Follows a **request-response** model.
- **Stateless**, **simple**, and **extensible**.


