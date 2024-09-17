# 🚀 Introduction to Docker

Docker is an open platform for developing, shipping, and running applications. Docker enables developers to package applications into containers—standardized executable components that combine application source code with the operating system libraries and dependencies required to run that code in any environment.

## Key benefits of Docker:

- **Portability**: Consistent environments from development to production.
- **Efficiency**: Lightweight containers that use fewer resources than virtual machines.
- **Isolation**: Each container runs independently without affecting others.

## 🛠 Core Docker Concepts

### 1. Docker Images
**Definition**: A Docker image is a read-only template used to create Docker containers. Images are built from Dockerfiles and can be shared via Docker Hub or private repositories.

**Components**:
- **Layers**: Images are composed of layers stacked on top of each other. Each layer represents a change or addition to the image.
- **Tags**: Tags (like `latest`, `v1.0`) are used to identify specific versions of an image.

### 2. Docker Containers
**Definition**: A Docker container is a runnable instance of a Docker image. Containers are lightweight and share the host OS kernel, but they are isolated from each other.

**Lifecycle**:
- **Creating**: Run a container using the `docker run` command.
- **Running**: Active state where the container executes its application.
- **Stopping**: Gracefully stopping the container using `docker stop`.
- **Removing**: Delete the container using `docker rm` once it is stopped.

### 3. Docker Engine
**Definition**: Docker Engine is the runtime that runs and manages Docker containers. It includes the Docker daemon, CLI (Command-Line Interface), and REST API.

### 4. Docker Hub
**Definition**: Docker Hub is a cloud-based registry service for sharing Docker images. It hosts public and private repositories where images can be pulled and pushed.

### 5. Dockerfile
**Definition**: A Dockerfile is a text file that contains a set of instructions to build a Docker image. It defines the base image, environment variables, file copies, and commands to execute.

### 6. Docker Compose
**Definition**: Docker Compose is a tool for defining and running multi-container Docker applications. With `docker-compose.yml`, you can configure application services, networks, and volumes in a single file.

### 7. Docker Volume
**Definition**: Docker volumes are used for persistent data storage. They are managed by Docker and can be shared between containers.

## 🔧 Basic Docker Commands

Below are some of the most commonly used Docker commands to get started:

### Run a container:

```bash
docker run <image>
```

This command pulls an image from Docker Hub (if not present locally) and runs it as a container.

### List running containers:

```bash
docker ps
```

Lists all currently running containers.

### Stop a running container:

```bash
docker stop <container_id>
```

Stops a running container.

### Remove a container:

```bash
docker rm <container_id>
```

Removes a stopped container.

### Execute a command inside a container:

```bash
docker exec -it <container_id> <command>
```

This is useful for entering the container and interacting with it directly, e.g., opening a bash shell.

### Pull an image:

```bash
docker pull <image>
```

Pulls the latest version of an image from Docker Hub to your local machine.

## 🌟 Example: Running an Nginx Web Server

Let’s start by running a simple web server using an Nginx container.

### Step 1: Run an Nginx container.

```bash
docker run -d -p 8080:80 nginx
```

This command pulls the Nginx image, runs it as a detached container (`-d`), and maps port 8080 on your host to port 80 inside the container (`-p 8080:80`).

### Step 2: Open your web browser and go to [http://localhost:8080](http://localhost:8080). You should see the default Nginx page.

### Step 3: Stop the Nginx container.

```bash
docker stop <container_id>
```

## 🧑‍💻 Exercises: Practicing Basic Docker Commands

### Run a Hello World Container:

```bash
docker run hello-world
```

What happens here? Docker pulls the hello-world image, creates a container, and prints a message.

### List All Running and Stopped Containers:

```bash
docker ps -a
```

View details about both active and inactive containers.

### Remove an Image:

```bash
docker rmi <image_id>
```

This removes an image from your local machine, but only if it’s not in use by a running container.

### Interactive Container: Run an Ubuntu container and enter its bash shell.

```bash
docker run -it ubuntu bash
```

You’re now inside an Ubuntu container. Try running some Linux commands!

## 🚧 What’s Next?

- Dive deeper into Docker by learning about Dockerfiles and custom images.
- Experiment with creating your own containerized applications.
