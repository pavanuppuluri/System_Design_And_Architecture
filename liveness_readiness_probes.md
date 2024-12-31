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
