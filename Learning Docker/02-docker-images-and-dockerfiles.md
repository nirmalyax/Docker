

# `02-docker-images-and-dockerfiles.md`

### Title: **Docker Images and Dockerfiles**

---

### 📦 What is a Docker Image?

A **Docker image** is a lightweight, standalone, and executable software package that includes everything needed to run an application: code, runtime, libraries, environment variables, and more.

- **Images are built in layers**: Each command in a Dockerfile creates a new layer in the image.
- **Immutability**: Once built, images are read-only.
- **Portability**: Images can run anywhere Docker is installed.

---

### 🖼️ Understanding Docker Images

#### Key Concepts:
- **Base Images**: The starting point for building your own images (e.g., `ubuntu`, `alpine`).
- **Parent-Child Relationship**: Each image is built from a parent image, which is the foundation layer.
- **Image Tags**: Images are identified by tags (e.g., `node:14`, `python:3.8`). Tags point to specific versions of the image.

#### Example:
```bash
docker pull nginx:latest
```
This pulls the latest version of the Nginx image from Docker Hub.

---

### 📝 Dockerfile: Building Your Own Image

A **Dockerfile** is a text file containing instructions to build a Docker image. It automates the process of creating images step by step.

#### Basic Dockerfile Syntax:
Each Dockerfile consists of several commands, which represent a step in the build process.

- **FROM**: Defines the base image.
- **RUN**: Executes a command inside the image.
- **COPY**: Copies files from the local machine to the image.
- **CMD**: Defines the default command to run in the container.
- **EXPOSE**: Informs Docker that the container listens on a specific port.

#### Example Dockerfile:

```dockerfile
# Step 1: Use a base image
FROM node:14

# Step 2: Set working directory in the container
WORKDIR /usr/src/app

# Step 3: Copy package.json and install dependencies
COPY package*.json ./
RUN npm install

# Step 4: Copy the rest of the application code
COPY . .

# Step 5: Expose the port the app runs on
EXPOSE 8080

# Step 6: Define the command to start the app
CMD ["node", "app.js"]
```

---

### 🔧 Building and Running a Custom Image

#### Step 1: Build the Image
Run the following command to build an image from your Dockerfile:
```bash
docker build -t my-node-app .
```
- **`-t my-node-app`**: Tags the image as `my-node-app`.
- **`.`**: The current directory is the build context (where your Dockerfile and app code are located).

#### Step 2: Run the Container
After building the image, you can run a container from it:
```bash
docker run -p 8080:8080 my-node-app
```
- **`-p 8080:8080`**: Maps port 8080 on the host to port 8080 in the container.

---

### 🛠️ Dockerfile Best Practices

1. **Use Official Base Images**: Start from minimal, verified base images like `alpine` or official language runtime images.
   ```dockerfile
   FROM python:3.8-slim
   ```

2. **Minimize Layers**: Each `RUN`, `COPY`, or `ADD` command creates a new layer. Combine commands to reduce the number of layers.
   ```dockerfile
   RUN apt-get update && apt-get install -y \
       curl \
       git
   ```

3. **Leverage `.dockerignore`**: Use a `.dockerignore` file to exclude unnecessary files from the build context, reducing the image size and build time.
   ```
   node_modules
   .git
   ```

4. **Use Multi-Stage Builds**: Multi-stage builds allow you to keep your final image small by copying only what’s necessary.
   ```dockerfile
   # Step 1: Build stage
   FROM golang:alpine AS builder
   WORKDIR /app
   COPY . .
   RUN go build -o myapp

   # Step 2: Final stage
   FROM alpine:latest
   WORKDIR /app
   COPY --from=builder /app/myapp .
   CMD ["./myapp"]
   ```

---

### 🌟 Example: Building a Simple Python App Image

Here’s a basic Dockerfile for a Python app using Flask:

```dockerfile
# Step 1: Use an official Python runtime as the base image
FROM python:3.8-slim

# Step 2: Set the working directory inside the container
WORKDIR /usr/src/app

# Step 3: Install the required dependencies
COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

# Step 4: Copy the source code into the container
COPY . .

# Step 5: Expose the port the app runs on
EXPOSE 5000

# Step 6: Run the application
CMD ["python", "app.py"]
```

To build and run this image:
```bash
docker build -t my-python-app .
docker run -p 5000:5000 my-python-app
```

---

### 🧑‍💻 Exercises: Docker Images and Dockerfiles

1. **Create a Custom Dockerfile**:
   - Build a Dockerfile for a basic Node.js app or any other language you are familiar with.

2. **Optimize Your Image**:
   - Try using multi-stage builds to reduce image size.

3. **Experiment with Dockerfile Commands**:
   - Use commands like `COPY`, `RUN`, `CMD`, and `EXPOSE` in your Dockerfile to understand how they interact.

---

### 🚧 What’s Next?

Now that you understand Docker images and Dockerfiles, it’s time to learn about **Docker Volumes** and **Networking** in the next topic!

