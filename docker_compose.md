# Docker Compose

**Docker Compose** is a tool for defining and managing multi-container Docker applications. It allows you to define an entire application's services, networks, and volumes in a single configuration file (`docker-compose.yml`). With Docker Compose, you can easily set up, manage, and scale applications that involve multiple containers, like a web server, database, cache, etc.

## Key Features of Docker Compose:
1. **Multi-container management**: Docker Compose allows you to run multiple Docker containers as a single application. Each container is typically a separate service (e.g., web server, database, cache).
   
2. **Declarative configuration**: The configuration of the containers is written in a simple YAML file, making it easy to define how the services interact with each other.

3. **Automation**: With Docker Compose, you can start, stop, and manage your multi-container application with a single command, simplifying the development workflow.

4. **Networking**: Compose automatically creates a default network for all the services defined in the `docker-compose.yml` file, allowing them to communicate with each other easily.

5. **Scaling**: Docker Compose allows you to scale services (like web servers) up or down by adjusting the number of containers running for a service.

## How Docker Compose Works:
1. **Define services**: In the `docker-compose.yml` file, you define all the services (containers) that your application needs. Each service can define its image, build context, environment variables, ports, volumes, and dependencies.

2. **Run commands**: Docker Compose provides commands like `docker-compose up`, `docker-compose down`, `docker-compose build`, and `docker-compose logs` to manage your application.

## Example of a `docker-compose.yml` file:

```yaml
version: '3'
services:
  web:
    image: nginx:latest
    ports:
      - "8080:80"
    volumes:
      - ./html:/usr/share/nginx/html

  db:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: example
    volumes:
      - db_data:/var/lib/mysql

  redis:
    image: redis:latest

volumes:
  db_data:
