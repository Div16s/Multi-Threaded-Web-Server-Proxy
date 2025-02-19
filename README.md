# Multi-Threaded Proxy Server with Caching

## Overview
This project is a **multi-threaded proxy web server with LRU caching**, implemented in **C**. The proxy server handles multiple client requests concurrently using threads, caches responses efficiently, and forwards requests to the actual remote server if a cache miss occurs.

## Features
- **Multi-threaded architecture** using **POSIX threads (pthreads)**
- **Socket programming** for handling client-server communication
- **LRU (Least Recently Used) caching** to improve response time
- **Efficient request parsing and forwarding**
- **Automatic cache updates** for newly fetched data

## Architecture
The architecture follows a **multi-threaded proxy model** where multiple clients connect to a proxy server, which either serves requests from its cache or fetches data from the actual remote server.

### Workflow
1. **Client requests** are received via a proxy socket.
2. The proxy checks its **LRU cache**:
   - If a **cache hit** occurs, the response is served from the cache.
   - If a **cache miss** occurs, the proxy forwards the request to the actual remote server.
3. The **actual remote server** sends the response back to the proxy.
4. The proxy:
   - **Updates the cache** with the new response.
   - **Forwards the response** to the client.
5. Each client request is handled by a **separate thread**, ensuring parallel processing.

### Architecture
```![Architecture]([https://github.com/user-attachments/assets/bc8abf2b-cecf-4a51-8a74-a18039d8cb1a](https://github.com/Div16s/Multi-Threaded-Web-Server-Proxy/blob/main/Multi-Threaded%20Proxy%20Web%20Server.png?raw=true))


```

## Technologies & Concepts Used
- **C Programming** for efficient low-level memory management
- **POSIX Threads (pthreads)** for multi-threading
- **Socket Programming** for client-server communication
- **LRU Cache Implementation** using linked lists/hashmaps
- **Makefile** for compiling the project in Linux/Ubuntu

## Installation & Usage
### Prerequisites
- Linux/Ubuntu environment
- `gcc` or `g++` compiler
- Basic knowledge of networking concepts

### Compiling the Project
Use the provided `Makefile` to compile the proxy server.

```sh
make
```

This will generate an executable `proxy`.

### Running the Proxy Server
Start the proxy server by running:
```sh
./proxy <port_number>
```
Example:
```sh
./proxy 8080
```

### Cleaning Up
To remove compiled files and reset the directory:
```sh
make clean
```

## Makefile Explanation
```make
CC=g++
CFLAGS= -g -Wall

all: proxy

proxy: proxy_server_cache.c
	$(CC) $(CFLAGS) -o proxy_parse.o -c proxy_parse.c -lpthread
	$(CC) $(CFLAGS) -o proxy.o -c proxy_server_cache.c -lpthread
	$(CC) $(CFLAGS) -o proxy proxy_parse.o proxy.o -lpthread

clean:
	rm -f proxy *.o
```
- **`CC=g++`**: Uses `g++` as the compiler.
- **`CFLAGS=-g -Wall`**: Enables debugging symbols (`-g`) and warnings (`-Wall`).
- **`proxy` target**:
  - Compiles `proxy_parse.c` and `proxy_server_cache.c` into object files.
  - Links object files into a final executable named `proxy`.
- **`clean` target** removes compiled files.

## Author
- **Divyankar Shah**  

