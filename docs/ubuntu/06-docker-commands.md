# Docker Commands for Ubuntu (WSL)

Essential Docker commands for containerizing data science applications and managing workflows.

## Installation & Setup

### Install Docker Engine (Native Ubuntu)
Recommended way for WSL2.
```bash
# 1. Setup repository
sudo apt update
sudo apt install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

# 2. Add repo to Apt sources
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo $VERSION_CODENAME) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# 3. Install packages
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### Post-Install: Run without sudo
```bash
# Add user to docker group
sudo usermod -aG docker $USER

# Apply changes (or restart terminal)
newgrp docker

# Test
docker ps
docker run hello-world
```

### Managing Docker Service (WSL)
```bash
sudo service docker start       # Start daemon
sudo service docker status      # Check if running
sudo service docker stop        # Stop daemon
```

## Basic Container Commands

### Running Containers
```bash
docker run hello-world                  # Run test image
docker run -it ubuntu bash              # Run interactive bash in Ubuntu
docker run -d -p 80:80 nginx            # Run detached (background) with port map
docker run --name myapp -d python       # Run with custom name
docker run --rm -it python              # Auto-remove container after exit
```

### Managing Containers
```bash
docker ps                    # List running containers
docker ps -a                 # List ALL containers (including stopped)
docker stop <id>             # Stop a container
docker start <id>            # Start a stopped container
docker restart <id>          # Restart a container
docker rm <id>               # Delete a container
docker rm -f $(docker ps -aq)  # Delete ALL containers
```

### Inspecting & Debugging
```bash
docker logs <id>             # See output/logs
docker logs -f <id>          # Follow logs live
docker inspect <id>          # Detailed config (JSON)
docker top <id>              # Processes inside container
docker exec -it <id> bash    # Open shell in RUNNING container
```

## Image Commands

### Working with Images
```bash
docker images                # List local images
docker pull python:3.11-slim # Download image from hub
docker rmi <id>              # Delete local image
docker rmi $(docker images -q)  # Delete ALL local images
docker tag myimage:latest user/repo  # Tag for upload
docker push user/repo        # Upload to Docker Hub
```

### Building Images
```bash
# Build from Dockerfile in current folder
docker build -t myapp:v1 .

# Build with specific file
docker build -f Dockerfile.dev -t myapp-dev .
```

## Dockerfile Essentials

Example for a Data Science App (Streamlit):

```dockerfile
# 1. Base image
FROM python:3.11-slim

# 2. Set working directory
WORKDIR /app

# 3. Copy requirements and install
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# 4. Copy project files
COPY . .

# 5. Network port
EXPOSE 8501

# 6. Startup command
CMD ["streamlit", "run", "app.py", "--server.port=8501", "--server.address=0.0.0.0"]
```

## Docker Compose

For multi-container projects (e.g., App + Database).

### Common Commands
```bash
docker compose up            # Start services
docker compose up -d         # Start in background
docker compose down          # Stop and remove everything
docker compose logs -f       # Follow logs
docker compose build         # Rebuild images
docker compose ps            # Status of services
```

Example `docker-compose.yml`:

```yaml
services:
  web:
    build: .
    ports:
      - "8501:8501"
  
  db:
    image: postgres:15
    environment:
      POSTGRES_PASSWORD: example
```

## Volumes & Networking

### Volumes (Persist Data)
```bash
# Mount local folder to container (for development)
docker run -v $(pwd):/app -p 8501:8501 myapp

# Named volume (managed by Docker)
docker volume create mydata
docker run -v mydata:/data postgres
```

### Networking
```bash
docker network ls            # List networks
docker network create mynet  # Create custom network
docker run --network mynet ... # Run in specific network
```

## Cleanup & Maintenance
```bash
docker system df             # Disk usage summary
docker system prune          # Remove unused data (safe)
docker system prune -a       # Remove ALL unused images
docker volume prune          # Remove unused volumes
docker image prune           # Remove dangling images
```

## Common DS/ML Docker Hub Images

- `python:3.11-slim` (General Python)
- `jupyter/datascience-notebook` (Jupyter stack)
- `tensorflow/tensorflow:latest-gpu` (TF + CUDA)
- `pytorch/pytorch` (PyTorch)
- `postgres` (Database)
- `redis` (Cache)

---
**Previous**: [Git & GitHub Commands](05-git-github-commands.md) | **Next**: [Quick Reference](quick-reference.md)
