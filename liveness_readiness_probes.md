# Liveness and Readiness Probes

- **Liveness Probe** checks if the application is running and not stuck.
- **Readiness Probe** checks if the application is ready to handle traffic.

<img width="1420" alt="image" src="https://github.com/user-attachments/assets/7faaea79-f663-463c-997e-ac04e3899af2" />


<img width="1133" alt="image" src="https://github.com/user-attachments/assets/911627f0-b0b1-418e-be22-17fadba04510" />

### Exposing the Health Endpoint

Spring Boot exposes the `/actuator/health` endpoint by default. This can be accessed to check the health of the application.

- **Liveness Probe**: `/actuator/health/livenessstate`
- **Readiness Probe**: `/actuator/health/readinessstate`

By default, Spring Boot's health endpoints are secured. You may need to expose them and configure their paths by editing the `application.yml` or `application.properties` file.

#### Example Configuration in `application.yml`:

```yaml
management:
  endpoints:
    web:
      exposure:
        include: health,info
  health:
    livenessstate:
      enabled: true
    readinessstate:
      enabled: true
```

### Deploying to docker-compose (Optional)

A Spring Boot application (for example, a microservice), which depends on a Config Server for configuration, is configured with liveness 
and readiness probes in a Docker Compose setup. 

In this case, the microservice depends on the Config Server being up and available to retrieve its configurations.

Here is how you can set up such a scenario in Docker Compose, where:

#### Example Docker Compose Setup:
In this example:

- The Config Server provides configuration to the Microservice via the Spring Cloud Config mechanism.
- The Microservice depends on the Config Server being available to retrieve its configuration.

`docker-compose.yml`

```
version: '3.8'

services:
  config-server:
    image: your-config-server-image:latest
    container_name: config-server
    ports:
      - "8888:8888"
    environment:
      - SPRING_PROFILES_ACTIVE=prod
    healthcheck:
      # Liveness Probe for Config Server
      test: ["CMD", "curl", "--fail", "http://localhost:8888/actuator/health/livenessstate"]
      interval: 30s
      retries: 3
      start_period: 10s
      timeout: 10s
    networks:
      - app-network

  microservice:
    image: your-microservice-image:latest
    container_name: microservice
    ports:
      - "8080:8080"
    environment:
      - SPRING_PROFILES_ACTIVE=prod
      - SPRING_CLOUD_CONFIG_URI=http://config-server:8888
    healthcheck:
      # Liveness Probe for Microservice
      test: ["CMD", "curl", "--fail", "http://localhost:8080/actuator/health/livenessstate"]
      interval: 30s
      retries: 3
      start_period: 10s
      timeout: 10s
    depends_on:
      config-server:
        condition: service_healthy
    networks:
      - app-network

networks:
  app-network:
    driver: bridge
```

#### How the Condition Works:
- When you use depends_on with condition: service_healthy, Docker will wait for the specified service (in this case, config-server) to be marked as healthy according to its health check before starting the dependent service (the microservice).
- If the Config Server is not healthy (for example, if it fails the health check), Docker will wait and not start the microservice.

### Deploying to Kubernetes (Optional)

When deploying your Spring Boot application to Kubernetes or a similar orchestrator, you can configure Kubernetes to check these probes for managing the application's lifecycle.

#### Example Kubernetes Configuration:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: spring-boot-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: spring-boot-app
  template:
    metadata:
      labels:
        app: spring-boot-app
    spec:
      containers:
      - name: spring-boot-app
        image: your-image
        ports:
        - containerPort: 8080
        livenessProbe:
          httpGet:
            path: /actuator/health/livenessstate
            port: 8080
          initialDelaySeconds: 10
          periodSeconds: 30
        readinessProbe:
          httpGet:
            path: /actuator/health/readinessstate
            port: 8080
          initialDelaySeconds: 10
          periodSeconds: 30
```
