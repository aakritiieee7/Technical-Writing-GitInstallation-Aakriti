# The Journey of a Web Request

When you type a URL in your browser and press Enter, a fascinating journey begins. Let's break down this journey step by step.

## 1. DNS Resolution
- The browser first needs to find the actual IP address of the server
- It checks various DNS caches (browser, operating system, router)
- If not found in caches, it queries DNS servers
- Finally gets the IP address of the server

**TODO:** Add explanation of DNS cache hierarchy and time complexity of DNS lookups

## 2. Establishing TCP Connection
- The browser initiates a TCP connection with the server
- This happens through the famous three-way handshake:
  - **TODO:**Complete the three-way handshake

**TODO:** Add details about TCP window sizing and congestion control algorithms

## 3. TLS Handshake (for HTTPS)
- After TCP connection, a secure channel needs to be established
- Client and server exchange certificates
- They negotiate encryption algorithms
- A secure connection is established

## 4. HTTP Request Formation
- Browser creates an HTTP request with:
  - **TODO:**Complete the request formation

# Common HTTP Headers Guide

### General Request Headers
These headers provide basic information about the request and client preferences. They help establish the foundation of HTTP communication between client and server.
- `Host`: Specifies domain name and port number
- `User-Agent`: Browser/client identification and capabilities
- `Accept`: Media types the client can process
- `Accept-Language`: Preferred natural languages
- `Accept-Encoding`: Supported compression algorithms
- `Connection`: Connection management options

### Authentication Headers
Authentication headers handle security credentials and session management. They ensure secure communication and maintain user sessions across requests.
- `Authorization`: Credentials for HTTP authentication
- `Cookie`: Previously stored cookies
- `WWW-Authenticate`: Authentication method required
- `Proxy-Authorization`: Credentials for proxy authentication

### Content Headers
Content headers describe the message body and its properties. They help servers understand how to process the incoming data.
- `Content-Type`: Media type of the request body
- `Content-Length`: Size of the request body in bytes
- `Content-Encoding`: Encoding applied to the body
- `Content-Language`: Natural language of the body
- `Content-Disposition`: How to present the response

### Caching Headers
Caching headers control how responses are stored and reused. They optimize performance by reducing unnecessary server requests.
- `Cache-Control`: Directives for caching mechanisms
- `If-Match`: Conditional request based on ETag
- `If-None-Match`: Opposite of If-Match
- `If-Modified-Since`: Conditional request based on timestamp
- `If-Unmodified-Since`: Opposite of If-Modified-Since
- `ETag`: Resource version identifier

### Security Headers
Security headers protect against various web vulnerabilities. They enforce security policies and prevent common attack vectors.
- `Origin`: Where the request originated
- `Referer`: URL of the previous web page
- `Sec-Fetch-Dest`: Request destination
- `Sec-Fetch-Mode`: Request mode
- `Sec-Fetch-Site`: Cross-origin request type

### Custom Headers
Custom headers extend standard HTTP functionality. They're often used for application-specific features and proxy services.
- `X-Requested-With`: Identifies AJAX requests
- `X-Forwarded-For`: Client IP when using proxy
- `X-Forwarded-Proto`: Original protocol (HTTP/HTTPS)
- `X-Real-IP`: Original client IP address

## Response Headers

### Status Headers
Status headers provide information about the server and response status. They help clients understand how to handle the response.
- `Access-Control-Allow-Origin`: CORS permissions
- `Allow`: Valid methods for the resource
- `Server`: Software used by the server

### Location Headers
Location headers manage redirects and resource locations. They guide clients to the correct resource location.
- `Location`: URL for redirection
- `Refresh`: Seconds until automatic redirect

### Caching Response Headers
These headers help clients manage cached responses effectively. They provide information about resource freshness and validity.
- `Age`: Time in seconds response has been cached
- `Expires`: Date/time after which response is stale
- `Last-Modified`: Last modification date of resource
- `Vary`: Headers that affect the response

### Security Response Headers
Security response headers protect against client-side vulnerabilities. They enforce browser security features and prevent common attacks.
- `Content-Security-Policy`: Security policy directives
- `Strict-Transport-Security`: HTTPS enforcement
- `X-Content-Type-Options`: MIME type adherence
- `X-Frame-Options`: Frame embedding permissions
- `X-XSS-Protection`: Cross-site scripting filter

## 5. Server Processing
- Request arrives at the server
- Server routes the request to appropriate handler
- Application logic processes the request
- Database queries may be executed
- Response is generated

## 6. Response Journey
### **HTTP Response Journey**  

Once the server receives an HTTP request, it processes it and sends back a structured response. This journey involves several steps:  

#### **1. Server Processing the Request**  
The server receives the request, extracts relevant details (method, URL, headers, and body), and determines how to respond.  
- If the request targets a static file (e.g., HTML, CSS), the server retrieves it from storage.  
- If it requires database access, the server queries the database and processes the data.  
- If it involves business logic (e.g., user authentication), the server executes the required functions.  

#### **2. Generating the HTTP Response**  
The server constructs a response containing:  
- **Status Line** – Includes the HTTP version, status code (e.g., `200 OK`, `404 Not Found`), and status message.  
- **Headers** – Metadata about the response (e.g., `Content-Type`, `Content-Length`, `Set-Cookie`).  
- **Body (if applicable)** – The actual content being sent, such as an HTML page, JSON data, or a file.  

**Example Response:**  
```
HTTP/1.1 200 OK  
Content-Type: text/html  
Content-Length: 1024  

<html>
  <body>Welcome to the website!</body>
</html>
```

#### **3. Data Transmission Back to the Browser**  
Once generated, the response travels back through the network:  
- **Server sends the response** over **TCP/IP** using the same connection established by the request.  
- **Packets travel** across the internet, moving through routers, switches, and ISPs.  
- **The browser receives the response**, reassembles packets, and processes the data.  

#### **4. Browser Rendering the Response**  
Upon receiving the response, the browser:  
- Reads the **status code** to determine success or failure.  
- Interprets **headers** (e.g., caching rules, content type).  
- Displays **HTML/CSS/JavaScript** or executes required actions (e.g., redirecting, prompting a download).  

If additional resources (images, stylesheets, scripts) are needed, the browser sends new requests, repeating the process.
## 7. Browser Processing
- Browser receives the response
- If HTML, begins parsing
- Downloads additional resources (CSS, JS, images)
- Renders the page

**TODO:** Add details about browser rendering pipeline and critical rendering path

## Common Optimization Techniques
- Content Delivery Networks (CDNs)
- Browser caching
- Compression
- Connection pooling

**TODO:** Add space and time complexity analysis for different caching strategies

## Error Scenarios
### **Error Scenarios in Web Requests**  

When a web request fails, the server responds with an **HTTP status code** indicating the issue. Below are common errors, their causes, and how to handle them on both the client and server sides.  

---

### **1. 404 Not Found**  
**Cause:**  
- The requested page, file, or API endpoint does not exist.  
- The URL is incorrect, broken, or the resource was removed.  

**Client-Side Handling:**  
- Check for typos in the URL.  
- Redirect users to a valid page (e.g., homepage or search page).  

**Server-Side Handling:**  
- Implement a **custom 404 page** with navigation options.  
- Ensure proper **URL routing** in the backend.  

---

### **2. 500 Internal Server Error**  
**Cause:**  
- A general server failure due to a bug, database issue, or misconfiguration.  

**Client-Side Handling:**  
- Show a **friendly error message** and suggest retrying later.  

**Server-Side Handling:**  
- Log errors for debugging.  
- Use **try-catch blocks** to handle failures gracefully.  

---

### **3. 403 Forbidden**  
**Cause:**  
- The user lacks permission to access the resource (e.g., admin-only pages).  

**Client-Side Handling:**  
- Display an **access denied message** with login suggestions.  

**Server-Side Handling:**  
- Enforce authentication and authorization rules.  
- Restrict access via backend configurations.  

---

### **4. 400 Bad Request**  
**Cause:**  
- The request has invalid syntax, missing parameters, or bad formatting.  

**Client-Side Handling:**  
- Validate inputs before sending the request.  
- Ensure API requests follow the expected format.  

**Server-Side Handling:**  
- Validate and sanitize user input.  
- Return clear error messages to help debugging.  

---

### **5. 401 Unauthorized**  
**Cause:**  
- Authentication is required but missing or invalid (e.g., expired token, incorrect credentials).  

**Client-Side Handling:**  
- Prompt the user to log in or refresh credentials.  

**Server-Side Handling:**  
- Implement authentication (JWT, OAuth, session-based).  
- Return appropriate headers for login guidance.  

---

### **6. 408 Request Timeout**  
**Cause:**  
- The client took too long to send a request, or the server took too long to respond.  

**Client-Side Handling:**  
- Retry the request after a short delay.  

**Server-Side Handling:**  
- Increase the timeout limit if needed.  
- Optimize server-side processing.  

---

This document provides a high-level overview of how web requests work. Several sections marked with **TODO** need additional details and technical depth. Contributions are welcome!
