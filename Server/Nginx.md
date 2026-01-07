# NGINX

**NGINX** (pronounced *“engine-x”*) is a **high-performance web server** and **reverse proxy** used to serve websites, APIs, and microservices at scale. It is widely deployed for **speed, stability, and low resource usage**.

<img width="3328" height="3900" alt="image" src="https://github.com/user-attachments/assets/bc60cd74-3d6a-4626-a0a1-b5a2df7a9ef8" />

## What NGINX actually does

At a practical level, NGINX can act as:

1. **Web Server**

   * Serves static content (HTML, CSS, JS) extremely fast
   * Often placed in front of application servers (Spring Boot, Node.js, etc.)

2. **Reverse Proxy**

   * Sits between users and your backend services
   * Hides internal services and routes requests securely

3. **Load Balancer**

   * Distributes traffic across multiple backend instances
   * Supports round-robin, least-connections, IP-hash, etc.

4. **API Gateway (lightweight)**

   * URL routing, rate limiting, headers, caching
   * Common in microservices architectures

5. **SSL / TLS Terminator**

   * Handles HTTPS so backend services can stay HTTP

## Why NGINX is so fast

NGINX uses an **event-driven, non-blocking architecture (A non-blocking architecture allows a program or system to initiate an operation (like I/O) and continue executing other tasks without waiting for it to finish.)**, unlike traditional thread-per-request servers.

**Result:**

* Handles **tens of thousands of concurrent connections**
* Uses **far less memory**
* Very stable under heavy load

## NGINX vs Apache (quick comparison)

| Feature          | NGINX        | Apache               |
| ---------------- | ------------ | -------------------- |
| Architecture     | Event-driven | Process/thread-based |
| High concurrency | Excellent    | Moderate             |
| Static files     | Very fast    | Slower               |
| Dynamic apps     | Via proxy    | Native modules       |
| Configuration    | Declarative  | Modular              |

**Rule of thumb:**

* High-traffic, APIs, microservices → **NGINX**
* Legacy shared hosting → Apache

## Typical real-world setup (Spring Boot example)

```
User
  ↓ HTTPS
NGINX (SSL + Routing)
  ↓ HTTP
Spring Boot App (8080)
```

NGINX:

* Terminates SSL
* Rate limits
* Load balances multiple Spring Boot instances

## Example: basic NGINX reverse proxy config

```nginx
server {
    listen 80;

    location / {
        proxy_pass http://localhost:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Forwarded-For $remote_addr;
    }
}
```

## Who uses NGINX

* Netflix, Airbnb, GitHub
* Kubernetes Ingress Controllers
* Cloud providers and CDNs
* Almost every high-scale backend system

The open-source project is maintained by **NGINX** (now part of F5).

## When you should use NGINX

Use it if you need:

* High performance & low latency
* Reverse proxy for Spring Boot / Node / Python
* Load balancing
* SSL offloading
* Production-grade traffic handling

Do **not** use it if:

* You are building a simple local app
* Your framework already embeds a server and scale is low

## One-line takeaway

> **NGINX is the front door of modern web systems — fast, scalable, and battle-tested.**

