

# `05-docker-swarm.md`

### Title: **Docker Swarm: Clustering and Orchestration**

---

### 🐝 What is Docker Swarm?

**Docker Swarm** is Docker’s native **container orchestration** tool that allows you to manage a cluster of Docker engines (nodes) and deploy services across them. It turns a group of Docker hosts into a single virtual Docker host, enabling distributed and scalable deployments.

---

### 🏗️ Why Use Docker Swarm?

- **Scalability**: Swarm allows you to easily scale your services by adding or removing containers across multiple nodes.
- **High Availability**: Swarm ensures that services remain available even if some nodes fail, by replicating services across different nodes.
- **Built-In Load Balancing**: Swarm automatically distributes network traffic to containers across the nodes in the cluster.
- **Declarative Service Model**: You define the desired state of your services (like the number of replicas), and Swarm ensures that the system matches that state.

---

### 🛠 Key Components of Docker Swarm

1. **Node**: A Docker engine participating in the Swarm cluster. It can be either a **manager** node or a **worker** node.
   - **Manager Node**: Responsible for the orchestration and management of the cluster. It maintains the desired state of the cluster.
   - **Worker Node**: Executes tasks assigned by the manager node. It does not make any orchestration decisions.
   
2. **Service**: Defines the tasks to run. In a Swarm, services are the containers that you deploy and manage.
   
3. **Task**: A single instance of a container, running as part of a service.
   
4. **Overlay Network**: A network that spans all the nodes in the Swarm and allows containers running on different nodes to communicate with each other.

---

### 🔌 How to Set Up a Docker Swarm

#### Step 1: Initialize the Swarm
On the manager node, initialize the Swarm:
```bash
docker swarm init --advertise-addr <MANAGER-IP>
```
The `--advertise-addr` flag specifies the IP address that other nodes should use to communicate with the manager.

#### Step 2: Add Worker Nodes
After initializing, Docker will give you a token. Run this command on the worker nodes to join the Swarm:
```bash
docker swarm join --token <WORKER-TOKEN> <MANAGER-IP>:2377
```

#### Step 3: Verify the Nodes
On the manager node, check the status of the Swarm:
```bash
docker node ls
```

---

### 📜 Example: Deploying a Service in Docker Swarm

Let’s deploy an Nginx service with 3 replicas:

1. **Deploy the service**:
   ```bash
   docker service create --name nginx-service --replicas 3 -p 80:80 nginx
   ```

2. **List running services**:
   ```bash
   docker service ls
   ```

3. **View service details**:
   ```bash
   docker service ps nginx-service
   ```

4. **Scale the service**:
   You can scale your service up or down as needed:
   ```bash
   docker service scale nginx-service=5
   ```

---

### 📊 Docker Swarm Networking

Swarm uses **overlay networks** to enable communication between services running on different nodes. When you deploy a service, it automatically connects to the Swarm’s default overlay network, but you can also define custom overlay networks.

#### Create an Overlay Network:
```bash
docker network create --driver overlay my-overlay-network
```

#### Attach a Service to the Network:
```bash
docker service create --name nginx-service --network my-overlay-network nginx
```

---

### 🤖 Managing Services in Docker Swarm

- **Update a Service**: You can update an existing service, for example, changing the image or environment variables:
   ```bash
   docker service update --image nginx:alpine nginx-service
   ```

- **Remove a Service**: If you want to remove a service:
   ```bash
   docker service rm nginx-service
   ```

- **Monitor Services**: You can inspect logs from a specific service to monitor its health:
   ```bash
   docker service logs nginx-service
   ```

---

### 🧠 Docker Swarm vs Kubernetes

Both Docker Swarm and Kubernetes are container orchestration platforms, but they differ in some key areas:

- **Ease of Use**: Docker Swarm is simpler and quicker to set up, making it great for smaller projects or teams with less orchestration experience.
- **Scalability**: Kubernetes is more feature-rich and suitable for large-scale, complex deployments.
- **Ecosystem**: Kubernetes has a larger and more active ecosystem with widespread industry adoption.
  
Docker Swarm is a solid choice for simpler, smaller-scale setups, while Kubernetes is typically used for more complex, enterprise-level orchestration.

---

### 🧑‍💻 Exercises: Working with Docker Swarm

1. **Set up a Swarm**: Create a Swarm cluster with one manager and two worker nodes. Deploy a service with multiple replicas and test failover by shutting down a worker node.
   
2. **Create a Custom Overlay Network**: Deploy services across different nodes in the Swarm and verify that they can communicate with each other via an overlay network.

3. **Scaling Services**: Deploy a service with 3 replicas, then scale it up to 6 replicas. Monitor how the load is distributed across the nodes.

---

