## Docker Commands FAQ

### Basic Commands
- **`docker ps`** — List running containers.
- **`docker pull <image>`** — Download an image from a registry.
- **`docker build -t <tag> .`** — Build an image from a Dockerfile.
- **`docker logs <container_id>`** — View logs of a container.
- **`docker run <image>`** — Start a container from an image.

### Container Management
- **`docker stop <container_id>`** — Stop a running container.
- **`docker kill <container_id>`** — Forcefully stop a container.
- **`docker rm <container_id>`** — Remove a stopped container.
- **`docker rmi <image>`** — Remove an unused image.
- **`docker volume ls`** — List all volumes.

### Docker Compose
- **`docker-compose up -d`** — Start services in detached mode.
- **`docker-compose down`** — Stop and remove containers, networks, and volumes.
- **`docker-compose logs`** — View logs of all services.

### Advanced
- **`docker exec -it <container_id> bash`** — Open an interactive shell in a running container.
- **`docker system prune`** — Remove unused data (images, containers, volumes and networks).
- **`docker image prune -a`** — Remove all unused images.
- **`docker logs <container_id> --since <time>`** — View logs from a specific time period (e.g., `--since 1h` for the last hour, `--since yyyy-dd-mmThh:mm:ss` for logs since a specific timestamp).
- **`docker logs <container_id> --until <time>`** — View logs up to a specific time (e.g., `--until yyyy-dd-mmThh:mm:ss` for logs until a specific timestamp).