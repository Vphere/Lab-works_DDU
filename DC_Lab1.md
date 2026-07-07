# Distributed Computing Systems Lab

# 1. Real-Life Application of Distributed Computing System

## Example: Netflix

### How Netflix Uses Distributed Computing

Netflix uses thousands of servers distributed across different geographical locations instead of a single server.

### Working

1. A user opens the Netflix application or website.
2. The request is sent to the nearest Netflix server.
3. If the requested content is available, streaming starts immediately.
4. Otherwise, another server in the distributed network provides the content.
5. Multiple servers work together to serve millions of users simultaneously.

### Advantages

- Scalability
- High Availability
- Fault Tolerance
- Load Balancing
- Low Latency

### Other Examples

- Google Search
- Amazon
- Facebook
- WhatsApp
- YouTube
- Banking Applications

---

# 2. Socket

## Definition

A **socket** is a communication endpoint identified by an **IP Address**, **Port Number**, and **Protocol (TCP/UDP)**. It enables applications to send and receive data over a network.

**Example**

- IP Address: 192.168.1.10
- Port Number: 8080

## Need of Socket

- Establish communication between client and server.
- Send and receive data.
- Support distributed applications.
- Enable communication using TCP or UDP.
- Allow multiple clients to communicate with a server simultaneously.

---

# 3. Applications of Socket

## Web Browsing

- Browser creates a socket.
- Connects to the web server.
- Sends an HTTP request.
- Receives the webpage.

## Chat Applications

- Connects to the messaging server.
- Sends and receives messages instantly.

## Video Streaming

- Connects to the streaming server.
- Receives video data continuously.

## Online Games

- Exchanges player actions and game updates in real time.

## File Transfer

- Transfers file packets between client and server.

---

# 4. Socket Programming Flow

## Server Side

```text
socket()
    ↓
bind()
    ↓
listen()
    ↓
accept()
    ↓
recv()/read()
    ↓
send()/write()
    ↓
close()
```

## Client Side

```text
socket()
    ↓
connect()
    ↓
send()/write()
    ↓
recv()/read()
    ↓
close()
```

---

# 5. Socket Functions

## 1. socket()

**Used On:** Server ✔ Client ✔

### Syntax

```c
int socket(int domain, int type, int protocol);
```

### Parameters

- **domain** → AF_INET (IPv4), AF_INET6 (IPv6)
- **type** → SOCK_STREAM (TCP), SOCK_DGRAM (UDP)
- **protocol** → 0 (Default)

### Purpose

Creates a communication endpoint (socket).

### What Happens?

**Server:** Creates a socket that will listen for client connections.

**Client:** Creates a socket that will connect to the server.

---

## 2. bind()

**Used On:** Server ✔

### Syntax

```c
int bind(int sockfd,
         const struct sockaddr *addr,
         socklen_t addrlen);
```

### Purpose

Associates the socket with an IP address and port number.

### What Happens?

**Server:** Registers its IP address and port number so clients know where to connect.

**Client:** Normally does not use `bind()` because the operating system automatically assigns a temporary port.

---

## 3. listen()

**Used On:** Server ✔

### Syntax

```c
int listen(int sockfd, int backlog);
```

### Purpose

Waits for incoming client connection requests.

### What Happens?

The server starts listening for clients and stores pending requests in a queue (specified by `backlog`).

---

## 4. connect()

**Used On:** Client ✔

### Syntax

```c
int connect(int sockfd,
            const struct sockaddr *addr,
            socklen_t addrlen);
```

### Purpose

Connects the client to the server.

### What Happens?

The client sends a connection request to the server. The server receives this request through `accept()`.

---

## 5. accept()

**Used On:** Server ✔

### Syntax

```c
int accept(int sockfd,
           struct sockaddr *addr,
           socklen_t *addrlen);
```

### Purpose

Accepts a client connection and creates a new socket dedicated to that client.

### What Happens?

The original server socket continues listening for new clients, while the new socket communicates with the connected client.

---

## 6. send() / write()

**Used On:** Server ✔ Client ✔

### Syntax

```c
int send(int sockfd,
         const void *buffer,
         size_t length,
         int flags);
```

or

```c
ssize_t write(int fd,
              const void *buffer,
              size_t count);
```

### Purpose

Sends data through the socket.

### What Happens?

- **Client:** Sends requests or data to the server.
- **Server:** Sends responses or data back to the client.

### Difference

- `send()` is specifically designed for sockets and supports additional flags.
- `write()` is a generic file I/O function but also works with sockets.

---

## 7. recv() / read()

**Used On:** Server ✔ Client ✔

### Syntax

```c
int recv(int sockfd,
         void *buffer,
         size_t length,
         int flags);
```

or

```c
ssize_t read(int fd,
             void *buffer,
             size_t count);
```

### Purpose

Receives data from the socket.

### What Happens?

- **Server:** Receives requests or data from the client.
- **Client:** Receives responses or data from the server.

### Difference

- `recv()` is socket-specific and supports flags.
- `read()` is a generic file I/O function but also works with sockets.

---

## 8. close()

**Used On:** Server ✔ Client ✔

### Syntax

```c
int close(int sockfd);
```

### Purpose

Closes the socket and releases all associated resources.

### What Happens?

- **Client:** Disconnects from the server.
- **Server:** Closes the communication socket after data transfer is complete.

---

# 6. End-to-End Communication

```text
CLIENT                                SERVER

socket() -------------------------> socket()

connect() ------------------------> bind()
                                    listen()
                                    accept()

send("Hello") --------------------> recv()

recv() <-------------------------- send("Welcome")

close() --------------------------> close()
```

---

# 7. Summary Table

| Function | Server | Client | Purpose |
|----------|:------:|:------:|---------|
| socket() | ✔ | ✔ | Creates a socket |
| bind() | ✔ | ✖ | Assigns IP address and port number |
| listen() | ✔ | ✖ | Waits for client connection requests |
| connect() | ✖ | ✔ | Connects to the server |
| accept() | ✔ | ✖ | Accepts a client connection |
| send() / write() | ✔ | ✔ | Sends data |
| recv() / read() | ✔ | ✔ | Receives data |
| close() | ✔ | ✔ | Closes the socket |
