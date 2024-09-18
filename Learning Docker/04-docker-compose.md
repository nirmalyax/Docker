
# `04-docker-compose.md`

### Title: **Docker Compose: Simplifying Multi-Container Applications**

---

### 🧩 What is Docker Compose?

**Docker Compose** is a tool for defining and running multi-container Docker applications. It allows you to manage and configure multiple containers using a single file (`docker-compose.yml`). Compose makes it easier to manage interconnected services (like a web server, database, and cache) that make up an application.

---

### 📜 Why Use Docker Compose?

- **Multi-Container Setup**: Manage multiple services (e.g., frontend, backend, database) in a single configuration.
- **Declarative Config**: All configurations are stored in a YAML file, making it easy to define services, networks, and volumes.
- **Reusability**: Simplifies reusing container configurations across development, testing, and production environments.
- **Ease of Use**: Use simple commands to bring up or down an entire application stack.

---

### 🛠 Key Concepts in Docker Compose

- **Service**: Represents a single container. You define the container image, ports, environment variables, and other settings.
- **Network**: Compose automatically creates a network to allow services to communicate with each other.
- **Volume**: You can define volumes to persist data across containers or services.
- **Compose File**: A YAML file that contains the configuration of your services, networks, and volumes.

---

### 📄 Example: Basic Docker Compose File

Here’s a simple `docker-compose.yml` file to run a web application using Nginx and Redis:

```yaml
version: '3'

services:
  web:
    image: nginx:latest
    ports:
      - "8080:80"
    volumes:
      - ./web:/usr/share/nginx/html
    networks:
      - my-network

  redis:
    image: redis:alpine
    networks:
      - my-network

networks:
  my-network:
    driver: bridge
```

---

### 🛠 Understanding the Docker Compose File

- **Version**: Specifies the version of Docker Compose (e.g., version: '3').
- **Services**:
  - **web**: Runs the Nginx web server.
    - `ports`: Maps port 80 in the container to port 8080 on the host.
    - `volumes`: Mounts the local `./web` directory to `/usr/share/nginx/html` in the container.
  - **redis**: Runs the Redis service using the `alpine` version.
- **Networks**: Defines a custom bridge network (`my-network`) for service communication.

---

### ⚙️ Basic Docker Compose Commands

- **Start services**:
  ```bash
  docker-compose up
  ```
  This command starts all services defined in the `docker-compose.yml` file.

- **Start services in detached mode**:
  ```bash
  docker-compose up -d
  ```
  Runs the containers in the background (detached).

- **Stop services**:
  ```bash
  docker-compose down
  ```
  This stops and removes the containers, networks, and volumes created by `up`.

- **View running services**:
  ```bash
  docker-compose ps
  ```

- **Check service logs**:
  ```bash
  docker-compose logs
  ```

---

### 🏗 Example: Multi-Container Web Application

Let’s say you want to run a multi-container application with a Flask web server and a PostgreSQL database. Here’s how you could define it using Docker Compose:

```yaml
version: '3.8'

services:
  web:
    image: python:3.8-slim
    command: python app.py
    volumes:
      - ./web:/usr/src/app
    ports:
      - "5000:5000"
    networks:
      - app-network
    depends_on:
      - db

  db:
    image: postgres:12
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
      POSTGRES_DB: mydatabase
    volumes:
      - pgdata:/var/lib/postgresql/data
    networks:
      - app-network

networks:
  app-network:
    driver: bridge

volumes:
  pgdata:
```

#### Explanation:
- **web**:
  - Uses the Python base image.
  - Runs the `app.py` file.
  - Exposes port 5000 on the host.
  - Depends on the `db` service (PostgreSQL), meaning the database will start first.
- **db**:
  - Runs PostgreSQL with custom environment variables for user, password, and database.
  - Persists data in the `pgdata` volume.

---

### 🔗 Service Dependencies

Using **`depends_on`** in Docker Compose allows you to define dependencies between services. In the example above, the web service depends on the db service, meaning the database will start before the web service.

---

### 📚 Docker Compose Best Practices

1. **Use Multi-Stage Builds**: Keep images lightweight by separating the build and runtime stages.
   ```yaml
   build:
     context: .
     dockerfile: Dockerfile
   ```

2. **Environment Variables**: Use environment files (`.env`) to manage sensitive information.
   ```yaml
   env_file:
     - .env
   ```

3. **Use Named Volumes**: Ensure data persists between container restarts by defining named volumes.
   ```yaml
   volumes:
     - db-data:/var/lib/postgresql/data
   ```

4. **Modular Compose Files**: Split your `docker-compose.yml` into multiple files for production and development configurations.

---

### 🧑‍💻 Exercises: Working with Docker Compose

1. **Build a Multi-Container App**:
   - Create a Docker Compose file that runs a frontend, backend, and database.
   - Set up proper networking and volume management.

2. **Use Environment Variables**:
   - Create a `.env` file and use environment variables to configure your services dynamically.

3. **Scale Services**:
   - Experiment with scaling by running multiple instances of a service.
   ```bash
   docker-compose up --scale web=3
   ```

---

### 🚧 What’s Next?

In the next topic, we will explore **Docker Swarm** and how it enables clustering and service orchestration for scalable, distributed applications.

