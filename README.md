# Docker Usage Guide

## 📦 Build an Image from a Dockerfile and Project Directory

```bash
docker build -t image-name ./project-dir
```
Builds a Docker image named `image-name` using the Dockerfile and contents inside `./project-dir` (the Dockerfile is also in this directory).

---

## 🚀 Create and Run a Container with a Mounted Directory

```bash
docker run -it --name container-name -v host-dir:container-dir image-name
```
- `-it`: Interactive terminal  
- `--name`: Assign a name to the container  
- `-v`: Mount a directory from host (`host-dir`) to container (`container-dir`)

---

## 🏗️ Only Create a Container (Do Not Start)

```bash
docker create --name container-name -v host-dir:container-dir image-name
```
Creates a container but does not start it.

---

## 🧠 Access a Running Container

```bash
docker exec -it <container-name/id> bash
```
- Runs a command (`bash`) in a running container  
- `-it`: Opens an interactive terminal session

---

## 🔁 Start a Stopped Container (Interactive Mode)

```bash
docker start -ai <container-name/id>
```
- `-a`: Attach STDOUT/STDERR  
- `-i`: Keep STDIN open

---

## 📋 List Containers

```bash
docker ps -a
```
- Lists all containers, including stopped ones  
- Omit `-a` to show only running containers

---

# ⚙️ docker-compose.yml

The `docker-compose.yml` file is a powerful tool that lets you define, configure, and run multi-container Docker applications. 
It uses a YAML syntax to configure your application's services, networks, and volumes.

- Inter-Service Networking

    All services defined in a `docker-compose.yml` file can access each other using:

    ```
    http://<target-service-name>:<port>
    ```
- Environment Variables
    Set environment variables for your services directly in the `docker-compose.yml` file.
- Orchestration
    With a single command (`docker compose up`), you can start, stop, and rebuild all services defined in your `docker-compose.yml`.
