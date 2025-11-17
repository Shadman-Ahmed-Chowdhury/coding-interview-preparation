# Backend Engineering Topics

This directory contains comprehensive notes and resources related to backend engineering. It covers various topics including server-side programming, database management, API development, authentication, and performance optimization which are most common to be asked in technical interviews.

## Contents
- [Backend Engineering Topics](#backend-engineering-topics)
  - [Contents](#contents)
  - [How Internet Works](#how-internet-works)
      - [What happens when you type a URL in your browser?](#what-happens-when-you-type-a-url-in-your-browser)
  - [Server \& Client Architecture](#server--client-architecture)
    - [Key Components:](#key-components)
  - [Difference Between **HTTP** and **HTTPS**](#difference-between-http-and-https)
  - [Difference Between **HTTP Call** and **Socket Call**](#difference-between-http-call-and-socket-call)
  - [Difference Between **REST** and **GraphQL**](#difference-between-rest-and-graphql)
  - [Difference Between **SQL** and **NoSQL**](#difference-between-sql-and-nosql)
  - [Difference Between **Authentication** and **Authorization**](#difference-between-authentication-and-authorization)
  - [Difference Between **Monolithic** and **Microservices** Architecture](#difference-between-monolithic-and-microservices-architecture)


## How Internet Works
The internet is a global network of interconnected computers that communicate using standardized protocols. It allows for the transfer of data and information across vast distances.

#### What happens when you type a URL in your browser?
1. **DNS Lookup**: The browser contacts a DNS server to resolve the domain name (e.g., www.example.com) into an IP address.
   1. First it goes to the local DNS cache (OS) to check if the IP address is already known.
   2. If not found, it queries the configured DNS servers (like ISP's DNS or public DNS like Google DNS) to get the IP address.
   3. If the DNS server has the record cached, it returns the IP address. Otherwise, it queries other DNS servers until it finds the IP address or gives up.
2. **Establishing a Connection**: The browser establishes a TCP connection with the server using the IP address.
   1. Three way handshake is performed to establish the connection between client and server.
   2. The client sends a SYN packet to the server, the server responds with a SYN-ACK packet, and the client sends an ACK packet back to the server.
   3. Once the handshake is complete, a TCP connection is established.
   4. If the URL uses HTTPS, an SSL/TLS handshake is performed to establish a secure connection.
3. **Sending an HTTP Request**: The browser sends an HTTP request to the server, asking for the specific resource (e.g., a web page).
4. **Server Processing**: The server processes the request, retrieves the requested resource, and prepares an HTTP response.
5. **Receiving the Response**: The browser receives the HTTP response from the server, which includes the requested resource (e.g., HTML, CSS, JavaScript).
6. **Rendering the Page**: The browser renders the web page using the received resources, displaying it to the user.
7. **Closing the Connection**: The TCP connection may be closed or kept alive for future requests. HTTP/1.1 and beyond support persistent connections which can be used later for multiple requests (JS/CSS/Images) with the same TCP connection.

[Back To Top ⬆️](#contents)

## Server & Client Architecture
In a client-server architecture, the client (usually a web browser) sends requests to the server, which processes those requests and sends back responses. The server hosts the application logic, databases, and other resources needed to fulfill client requests.
### Key Components:
- **Client**: The user interface that interacts with the server (e.g., web browser
  - Sends HTTP requests to the server
  - Receives and renders HTTP responses
- **Server**: The backend system that processes client requests
  - Listens for incoming requests
  - Processes requests using application logic
  - Interacts with databases to retrieve or store data
  - Sends HTTP responses back to the client 
- **Database**: A system that stores and manages data for the application
  - Can be relational (e.g., MySQL, PostgreSQL) or non-relational (e.g., MongoDB, Redis)
  - The server interacts with the database to perform CRUD (Create, Read, Update, Delete) operations
  - Ensures data integrity and consistency
  - Optimizes data retrieval and storage for performance
  - Handles concurrent access from multiple clients
  - Implements backup and recovery mechanisms to prevent data loss
  - Supports indexing and querying for efficient data access
- **APIs**: Application Programming Interfaces that allow communication between different software components
  - RESTful APIs are commonly used in web applications
  - Define endpoints for various operations (e.g., GET, POST, PUT, DELETE)
  - Facilitate data exchange between client and server

[Back To Top ⬆️](#contents)

Below is a **clean, compact, interview-friendly notes sheet** with **tables** where they make sense. You can use this as a quick revision guide.

---

## Difference Between **HTTP** and **HTTPS**

| Feature         | HTTP                         | HTTPS                                  |
| --------------- | ---------------------------- | -------------------------------------- |
| Security        | Not encrypted                | Encrypted using SSL/TLS                |
| Port            | 80                           | 443                                    |
| Data Protection | Vulnerable to MITM, sniffing | Protects against MITM, sniffing        |
| URL Prefix      | http://                      | https://                               |
| Certificate     | No certificate required      | Requires SSL certificate               |
| Use Case        | Non-sensitive data           | Sensitive data (payments, login, APIs) |

**Summary:** HTTPS = HTTP + Encryption + Security + Trust.

[Back To Top ⬆️](#contents)

## Difference Between **HTTP Call** and **Socket Call**

| Feature           | HTTP Call                             | Socket Call (WebSocket)                   |
| ----------------- | ------------------------------------- | ----------------------------------------- |
| Connection Type   | Stateless, one request → one response | Persistent connection                     |
| Direction         | Unidirectional (client → server)      | Bidirectional (client ↔ server)           |
| Real-Time Support | Not suitable for real-time            | Ideal for real-time apps                  |
| Protocol          | HTTP/HTTPS                            | WS/WSS                                    |
| Overhead          | Higher overhead per request           | Low overhead once connected               |
| Use Cases         | REST APIs, websites                   | Chat, live updates, notifications, gaming |

**Summary:**
HTTP = request/response.
WebSocket = continuous real-time communication.

[Back To Top ⬆️](#contents)

## Difference Between **REST** and **GraphQL**

| Feature             | REST                 | GraphQL                                        |
| ------------------- | -------------------- | ---------------------------------------------- |
| Data Fetching       | Multiple endpoints   | Single endpoint                                |
| Over/Under Fetching | Common               | Eliminated — client asks exactly what it needs |
| Response Format     | Fixed structure      | Flexible — client defines structure            |
| Versioning          | Often needed         | No versioning required                         |
| Performance         | Multiple round trips | One optimized query                            |
| Learning Curve      | Easier               | Slightly harder                                |

**Summary:**
REST = multiple endpoints, fixed responses.
GraphQL = one endpoint, client-controlled data.

[Back To Top ⬆️](#contents) 

## Difference Between **SQL** and **NoSQL**

| Feature        | SQL Databases                        | NoSQL Databases                           |
| -------------- | ------------------------------------ | ----------------------------------------- |
| Structure      | Relational, table-based              | Document, key-value, graph, column        |
| Schema         | Strict schema                        | Schema-less                               |
| Scalability    | Vertical scaling                     | Horizontal scaling                        |
| ACID Support   | Strong                               | Varies (eventual consistency)             |
| Query Language | SQL                                  | No standard query language                |
| Use Cases      | Banking, ERP, consistency heavy apps | Real-time, big data, flexible schema apps |

**Summary:**
SQL = structured, relational, consistent.
NoSQL = flexible, scalable, high performance.

[Back To Top ⬆️](#contents)

## Difference Between **Authentication** and **Authorization**

| Feature   | Authentication             | Authorization          |
| --------- | -------------------------- | ---------------------- |
| Meaning   | Who you are                | What you can access    |
| Validates | Identity                   | Permissions            |
| Happens   | First                      | After authentication   |
| Example   | Login using email/password | Access admin dashboard |

**Summary:**
Authentication = identity verification.
Authorization = access control.

[Back To Top ⬆️](#contents)

## Difference Between **Monolithic** and **Microservices** Architecture

| Feature         | Monolithic                  | Microservices                                  |
| --------------- | --------------------------- | ---------------------------------------------- |
| Structure       | Entire app in one codebase  | App broken into independent services           |
| Deployment      | Single deployment           | Independent deployments                        |
| Scaling         | Whole app scales together   | Individual services scale independently        |
| Technology      | Usually one tech stack      | Different stacks per service                   |
| Complexity      | Easier to develop initially | More complex (distributed system)              |
| Fault Isolation | Poor                        | Strong — one service failure doesn’t break all |
| Communication   | Internal method calls       | Network-based (HTTP, RPC, events)              |

**Summary:**
Monolithic = one big system, simple but less scalable.
Microservices = independent services, flexible but complex.

[Back To Top ⬆️](#contents)
