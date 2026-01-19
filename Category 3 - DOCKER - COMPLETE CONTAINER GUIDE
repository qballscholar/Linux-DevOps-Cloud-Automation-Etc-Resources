**════════════════════════════════════════════════════════════════════**  
**CATEGORY 3: DOCKER \- COMPLETE CONTAINER GUIDE**  
**════════════════════════════════════════════════════════════════════**

**Covering: 6-day Docker series including installation, 50+ commands, volumes, professional guide, and ELK stack deployment**

**/\* COMMENT: Docker revolutionized application deployment by containerizing apps with**  
   **their dependencies. Containers are lightweight, portable, and consistent across**  
   **environments. Docker is fundamental to modern DevOps practices. \*/**

**3.1 DOCKER FUNDAMENTALS**

**WHY DOCKER?**

**● Consistency: "Works on my machine" problem solved**  
**● Isolation: Applications run in isolated environments**  
**● Portability: Run anywhere \- laptop, cloud, on-prem**  
**● Resource Efficiency: Containers share OS kernel (vs VMs)**  
**● Fast Startup: Seconds vs minutes for VMs**  
**● Version Control: Images are versioned and immutable**

**DOCKER ARCHITECTURE:**

**Docker Client (CLI) → Docker Daemon (dockerd) → Containers**  
                  **↓**  
           **Docker Registry (Docker Hub, private registries)**

**Key Components:**  
**\- Images: Read-only templates (blueprints)**  
**\- Containers: Running instances of images**  
**\- Volumes: Persistent data storage**  
**\- Networks: Container communication**  
**\- Registry: Image storage and distribution**

**INSTALLATION:**

**\# RHEL/CentOS**  
**sudo yum install \-y yum-utils**  
**sudo yum-config-manager \--add-repo https://download.docker.com/linux/centos/docker-ce.repo**  
**sudo yum install docker-ce docker-ce-cli containerd.io**  
**sudo systemctl start docker**  
**sudo systemctl enable docker**

**\# Ubuntu**  
**sudo apt update**  
**sudo apt install apt-transport-https ca-certificates curl software-properties-common**  
**curl \-fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add \-**  
**sudo add-apt-repository "deb \[arch=amd64\] https://download.docker.com/linux/ubuntu $(lsb\_release \-cs) stable"**  
**sudo apt update**  
**sudo apt install docker-ce**

**\# Add user to docker group (avoid sudo)**  
**sudo usermod \-aG docker $USER**

**ESSENTIAL DOCKER COMMANDS:**

**/\* COMMENT: These 50+ commands cover 90% of daily Docker operations. Master these**  
   **for efficient container management. \*/**

**\# IMAGE MANAGEMENT**  
**docker images                      \# List images**  
**docker pull nginx:latest           \# Download image**  
**docker build \-t myapp:1.0 .        \# Build from Dockerfile**  
**docker tag myapp:1.0 myapp:latest  \# Tag image**  
**docker push myregistry/myapp:1.0   \# Push to registry**  
**docker rmi image\_id                \# Remove image**  
**docker image prune \-a              \# Remove unused images**

**\# CONTAINER OPERATIONS**  
**docker run \-d \--name web \-p 80:80 nginx  \# Run container**  
**docker ps                          \# List running containers**  
**docker ps \-a                       \# List all containers**  
**docker stop container\_name         \# Stop container**  
**docker start container\_name        \# Start container**  
**docker restart container\_name      \# Restart container**  
**docker rm container\_name           \# Remove container**  
**docker rm \-f $(docker ps \-aq)      \# Remove all containers**

**\# CONTAINER INSPECTION**  
**docker logs container\_name         \# View logs**  
**docker logs \-f container\_name      \# Follow logs (tail \-f)**  
**docker exec \-it container\_name bash  \# Enter container**  
**docker inspect container\_name      \# Detailed info (JSON)**  
**docker stats                       \# Resource usage**  
**docker top container\_name          \# Running processes**

**\# DOCKER RUN OPTIONS**  
**docker run \-d \\                    \# Detached mode**  
  **\--name myapp \\                   \# Container name**  
  **\-p 8080:80 \\                     \# Port mapping (host:container)**  
  **\-v /data:/app/data \\             \# Volume mount**  
  **\-e ENV\_VAR=value \\               \# Environment variable**  
  **\--restart unless-stopped \\       \# Restart policy**  
  **\--memory="500m" \\                \# Memory limit**  
  **\--cpus="1.5" \\                   \# CPU limit**  
  **nginx:latest**

**\# NETWORKING**  
**docker network ls                  \# List networks**  
**docker network create mynetwork    \# Create network**  
**docker run \--network=mynetwork app \# Connect to network**  
**docker network inspect mynetwork   \# Network details**

**\# VOLUMES**  
**docker volume ls                   \# List volumes**  
**docker volume create myvolume      \# Create volume**  
**docker volume inspect myvolume     \# Volume details**  
**docker volume rm myvolume          \# Remove volume**

**\# CLEANUP**  
**docker system prune                \# Remove unused data**  
**docker system prune \-a \--volumes   \# Aggressive cleanup**  
**docker system df                   \# Disk usage**

**3.2 DOCKERFILE BEST PRACTICES:**

**/\* COMMENT: Dockerfiles define how to build images. Following best practices results**  
   **in smaller, more secure, and faster-building images. \*/**

**\# Example Dockerfile**  
**FROM node:18-alpine                \# Use specific, slim base images**

**WORKDIR /app                       \# Set working directory**

**\# Copy package files first (caching)**  
**COPY package\*.json ./**  
**RUN npm ci \--only=production       \# Install dependencies**

**\# Copy application code**  
**COPY . .**

**\# Create non-root user**  
**RUN addgroup \-g 1001 \-S nodejs && \\**  
    **adduser \-S nodejs \-u 1001**  
**USER nodejs                        \# Run as non-root**

**EXPOSE 3000                        \# Document port**

**CMD \["node", "server.js"\]          \# Start command**

**Best Practices:**  
**✓ Use official base images**  
**✓ Use specific tags, not 'latest'**  
**✓ Minimize layers (combine RUN commands)**  
**✓ Leverage build cache (copy package files first)**  
**✓ Use .dockerignore file**  
**✓ Run as non-root user**  
**✓ Use multi-stage builds for smaller images**  
**✓ Scan images for vulnerabilities**

**3.3 DOCKER COMPOSE:**

**/\* COMMENT: Docker Compose orchestrates multi-container applications using YAML files.**  
   **Essential for local development and testing multi-service applications. \*/**

**\# docker-compose.yml example**  
**version: '3.8'**

**services:**  
  **web:**  
    **image: nginx:alpine**  
    **ports:**  
      **\- "80:80"**  
    **volumes:**  
      **\- ./html:/usr/share/nginx/html**  
    **depends\_on:**  
      **\- api**  
    **networks:**  
      **\- frontend**  
    
  **api:**  
    **build: ./api**  
    **environment:**  
      **\- DB\_HOST=database**  
      **\- DB\_PORT=5432**  
    **depends\_on:**  
      **\- database**  
    **networks:**  
      **\- frontend**  
      **\- backend**  
    
  **database:**  
    **image: postgres:15-alpine**  
    **environment:**  
      **\- POSTGRES\_PASSWORD=secretpass**  
    **volumes:**  
      **\- db\_data:/var/lib/postgresql/data**  
    **networks:**  
      **\- backend**

**volumes:**  
  **db\_data:**

**networks:**  
  **frontend:**  
  **backend:**

**\# Docker Compose commands**  
**docker-compose up \-d              \# Start all services**  
**docker-compose down               \# Stop and remove**  
**docker-compose ps                 \# List services**  
**docker-compose logs \-f            \# View logs**  
**docker-compose exec web sh        \# Execute command**  
**docker-compose build              \# Build images**  
**docker-compose restart            \# Restart services**
