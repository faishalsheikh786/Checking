# 🐳 Docker Complete Notes

A complete guide to understanding and working with Docker, Docker Compose, and essential commands.

---

## 🐋 What is Docker?
Docker is a platform that lets you **build, ship, and run applications in isolated environments** called containers.

Think of it like this:

- **Without Docker** → Your app runs directly on your computer, and you must install dependencies (Python, Node.js, libraries, etc.) manually.
- **With Docker** → Your app and all its dependencies are packaged together, so it runs the same way everywhere — on your laptop, a server, or in the cloud.

---

## ⚙️ What is Docker & Daemon?
The **Docker Daemon** (`dockerd`) is the background service that manages Docker objects:

- Builds images
- Runs containers
- Handles networking
- Manages volumes

You interact with Docker through the **Docker CLI** (command-line interface), which communicates with the daemon.

**Flow:**
```
You → Docker CLI → Docker Daemon → Containers/Images
```

---

## 📦 What is a Docker Image?
A **Docker image** is like a **blueprint** or **template** for containers.  
It contains everything your app needs to run:

- Operating system (like Ubuntu or Alpine)
- Application code
- Libraries and dependencies
- Configuration instructions

Example:
```bash
docker pull ubuntu
```
This downloads the Ubuntu Linux image from Docker Hub.

---

## 🚀 What is a Docker Container?
A **container** is a **running instance** of an image.

- When you run an image, Docker creates a container from it.
- It’s isolated from your system but can communicate through defined channels.
- You can start, stop, restart, or delete containers freely.

🧠 Analogy:
```
Image = Class / Blueprint
Container = Object / Instance
```

Example:
```bash
docker run -it ubuntu bash
```

---

## 🌐 What is Port Mapping?
Containers have isolated networks.  
To access apps inside a container, you use **port mapping**.

Example:
```bash
docker run -p 8080:80 nginx
```
- **8080** → Host (your machine) port
- **80** → Container port

Visit: [http://localhost:8080](http://localhost:8080)

---

## 🧱 What Does “Dockerize” Mean?
To **Dockerize** an application means to **package it (and all its dependencies)** into a Docker image so it can run in any environment.

---

## ⚡ Caching in Docker
When Docker builds an image, it uses **layer caching** to avoid redoing work.

Example `Dockerfile`:
```dockerfile
FROM node:18
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
ENTRYPOINT ["node", "main.js"]
```

Layers (cached separately):
1. Base image (node:18)
2. Work directory creation
3. Copy dependencies (`package.json`)
4. Install packages
5. Copy source files

If `package.json` doesn't change, Docker skips `npm install` using cache — saving build time.

---

## 🐳 What is Docker Compose?
**Docker Compose** is a tool to define and run **multi-container applications** with a single YAML file (`docker-compose.yml`).

Instead of manually starting each container, define them once and run:
```bash
docker compose up
```

Compose handles:
- Creating containers
- Networking
- Volumes (persistent data)
- Environment variables
- Container dependency order

Example:
```yaml
version: '3.8'

services:
  postgres:
    image: postgres
    ports:
      - '5432:5432'
    environment:
      POSTGRES_USER: postgres
      POSTGRES_DB: review
      POSTGRES_PASSWORD: password

  redis:
    image: redis
    ports:
      - '6379:6379'
```

Commands:
```bash
docker compose up        # Start containers
docker compose up -d     # Run in background
docker compose down      # Stop and remove containers
```

---

## 🧰 Common Docker Commands

| Command | Description |
|----------|--------------|
| `docker` | Check if Docker is installed |
| `docker -v` | Show Docker version |
| `docker run -it <image>` | Run an image interactively (downloads if not present) |
| `docker container ls` | List running containers |
| `docker container ls -a` | List all containers (including stopped) |
| `docker start <container>` | Start a stopped container |
| `docker stop <container>` | Stop a running container |
| `docker exec -it <container> bash` | Open an interactive shell in a container |
| `docker image ls` | List all downloaded images |
| `docker build -t <image-name> <path>` | Build an image from a Dockerfile |
| `docker run -p <host-port>:<container-port> <image>` | Map container port to host |
| `docker run -e key=value` | Pass environment variables to a container |
| `docker compose up` | Start services defined in docker-compose.yml |
| `docker compose down` | Stop and remove services |

---

## 🧠 Important Notes
- Containers do **not share data** — only the image is shared.
- Always prefer **official** and **verified** Docker Hub images.
- Third-party images can contain vulnerabilities — use caution.

---

📚 **Summary**
| Concept | Description |
|----------|-------------|
| **Image** | Blueprint for containers |
| **Container** | Running instance of an image |
| **Daemon** | Background service managing containers |
| **Port Mapping** | Expose container ports to host machine |
| **Docker Compose** | Tool for running multi-container apps |
| **Dockerize** | Packaging an app into a Docker image |

---

💙 **Author:** Your Name  
📅 **Last Updated:** November 2025

Happy Dockering! 🐳
