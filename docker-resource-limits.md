# Resource Limits in Docker

In Docker, you can specify resource limits such as CPU and memory for your containers. These limits help ensure that a container doesn't use more resources than necessary, preventing it from affecting other containers or the host system.

Here’s a detailed example of how to deploy a container with resource limits using Docker CLI and Docker Compose.

### Resource Limits in Docker CLI
When running a container via the Docker CLI, you can use the --memory and --cpus flags to set memory and CPU limits.

```
docker run -d \
  --name myapp \
  --memory="512m" \
  --cpus="1.0" \
  myapp-image
```

### Resource Limits in Docker Compose
You can specify resource limits for services defined in a docker-compose.yml file using the deploy.resources section. 
**Note**: Resource limits are only supported in Docker Swarm mode.

Example `docker-compose.yml`:

```
version: '3.8'

services:
  myapp:
    image: myapp-image
    deploy:
      resources:
        limits:
          memory: 512M
          cpus: '1.0'
        reservations:
          memory: 256M
          cpus: '0.5'
    ports:
      - "8080:8080"
```

### Scaling and Resource Limits in Docker Swarm
In a Docker Swarm environment, you can also scale services while applying resource limits. 
Docker will respect the CPU and memory constraints while scaling the service.

Example 'docker-compose.yml` with Scaling:

version: '3.8'

services:
  myapp:
    image: myapp-image
    deploy:
      replicas: 3  # Scale the service to 3 replicas
      resources:
        limits:
          memory: 512M
          cpus: '1.0'
        reservations:
          memory: 256M
          cpus: '0.5'
    ports:
      - "8080:8080"


## Monitoring Resource Usage
You can monitor the resource usage of containers using the `docker stats` command, which shows real-time metrics like CPU, memory, and network usage.

```
docker stats myapp
```

This will provide live statistics on the myapp container, including its memory and CPU usage, helping you see if the container is staying within its limits.


