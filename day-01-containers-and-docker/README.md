# Day 01 — Containers and Docker Fundamentals

> **Kubernetes Zero to Production** · Foundations

![Day 01: Traditional deployment](images/01-deployment.svg)

## 1. How applications run on a server

An application needs an environment in which to run. A web application, for example, may require a particular runtime (Java, Node.js, Python, etc.), operating-system libraries, configuration, and network access.

In a traditional deployment, the application and its dependencies are installed directly on a server. This works, but it becomes harder to maintain when different applications need different versions of the same dependencies.

**Example:** App A requires Python 3.10, while App B requires Python 3.12. Managing both on the same host requires careful isolation and dependency management.

**Common challenges**
- Differences between development, testing, and production environments
- Dependency conflicts between applications
- Reproducing a working setup on a new server
- Consistent deployment and rollback

Containers are one way to address these challenges.

## 2. Virtual machines and containers

![VMs and containers](images/02-vm-container.svg)

A **virtual machine (VM)** virtualizes hardware. Each VM normally runs its own guest operating system on a hypervisor.

A **container** is an isolated process (or group of processes) running on a host operating system. Linux containers use features such as namespaces and cgroups for isolation and resource control. Containers on the same Linux host share the host's kernel.

| | Virtual machine | Container |
|---|---|---|
| Isolation | Separate guest OS and virtualized hardware | Process-level isolation using OS features |
| Operating system | Guest OS per VM | Shares host kernel |
| Startup | Often slower | Often faster |
| Footprint | Typically larger | Typically smaller |
| Best fit | Stronger isolation boundaries, different guest OSes | Consistent packaging and efficient application deployment |

**Important:** Containers are isolated, but not identical to VMs in their security boundary. They also don't package their own Linux kernel.

## 3. What is a container image?

A **container image** is a packaged template that includes an application's filesystem content, required user-space dependencies, and metadata such as its default command.

A **container** is an instance created from an image. It can be started, stopped, inspected, and removed.

For example, one Nginx image can be used to start several separate Nginx containers.

## 4. What is Docker?

Docker provides tooling to build container images, manage images, and create and run containers.

![Docker workflow](images/03-docker-workflow.svg)

- **Dockerfile:** Text instructions used to build an image.
- **Docker image:** Packaged application and its dependencies.
- **Docker container:** An instance created from an image.
- **Registry:** A place to store and distribute images (Docker Hub is one example).

### A simple Dockerfile

```dockerfile
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
```

This image starts from Nginx and replaces its default landing page with your own `index.html`. The base image already supplies the server's default startup command.

## 5. Hands-on lab: Run Nginx with Docker

**Prerequisite:** Docker Engine or Docker Desktop installed and running. The commands below assume Docker CLI access.

### Step 1 — Check Docker

```bash
docker version
docker info
```

`docker version` shows client/server version details when the daemon is reachable. `docker info` shows information about the Docker environment.

### Step 2 — Download the image

```bash
docker pull nginx:alpine
docker images
```

### Step 3 — Start a container

```bash
docker run -d --name day01-nginx -p 8080:80 nginx:alpine
```

- `-d` runs in detached mode.
- `--name` gives the container a recognizable name.
- `-p 8080:80` publishes host port 8080 to container port 80.

Open **http://localhost:8080** in your browser. If Docker runs on a remote server, use the server's reachable IP or hostname and ensure the network/firewall permits access.

### Step 4 — Inspect the running container

```bash
docker ps
docker logs day01-nginx
docker inspect day01-nginx
```

To view processes in the container:

```bash
docker exec day01-nginx ps
```

### Step 5 — Stop, restart, and remove

```bash
docker stop day01-nginx
docker start day01-nginx
docker stop day01-nginx
docker rm day01-nginx
```

After removal, `docker ps -a` should no longer list `day01-nginx`.

> **Troubleshooting:** If port 8080 is already in use, replace `8080` with another available host port (for example, `8081`) and update the browser URL accordingly.

## 6. Why Docker alone isn't the full solution

![Manual management challenges](images/04-why-orchestration.svg)

Docker makes it easier to package and run applications, but running a growing application involves more than starting containers.

Consider a shopping website with multiple replicas running on several servers:

- Who decides which server should run each replica?
- What happens if a container or server fails?
- How do we deploy a new version gradually?
- How do we keep the requested number of replicas running?
- How should traffic reach healthy application instances?

These are **orchestration** problems. Kubernetes provides APIs and controllers to help coordinate workloads across a cluster.

**Important distinction:** Kubernetes uses container runtimes that implement the Container Runtime Interface (CRI), commonly containerd or CRI-O. Kubernetes does **not** require Docker Engine to run containers.

## 7. Quick recap

- An application needs a runtime environment and dependencies.
- VMs have their own guest operating systems; Linux containers share the host kernel.
- An image is a template; a container is an instance of that image.
- Docker helps build, distribute, and run container images.
- Running containers is not the same as orchestrating workloads across multiple servers.

**Next lesson:** Day 02 — Why Do We Need Kubernetes?

---

### References
- [Docker — Get started](https://docs.docker.com/get-started/)
- [Docker — What is a container?](https://www.docker.com/resources/what-container/)
- [Kubernetes — Container runtimes](https://kubernetes.io/docs/setup/production-environment/container-runtimes/)

