# Refresh configurations at runtime using refresh/path

<img width="1355" alt="image" src="https://github.com/user-attachments/assets/e37ba80b-2d0c-47f8-8a28-ca952bf64bb7" />

<br>
<br>
<br>

<img width="1311" alt="image" src="https://github.com/user-attachments/assets/7d0d8fd3-0b8d-4493-9531-b6552a0457c0" />


#### You invoked the refresh mechanism on Accounts service. and it worked fine. But how about in production where there may be multiple services? If a project has many microservices, then team may prefer to have an automated and efficient method of refreshing configuration instead of manually triggering each application instance. Let's evaluate other options that we have

## Refresh configurations at runtime using Spring Cloud Bus

# Spring Cloud Bus Example

Spring Cloud Bus is a powerful tool that allows applications to communicate with each other in a microservices architecture. It connects different services via an event bus to propagate configuration changes, events, and messages between services.

### Key Concepts
1. **Spring Cloud Bus** works by connecting services with a lightweight message broker (like RabbitMQ or Kafka). When one service publishes an event, the bus ensures that other services can consume that event and take appropriate actions.
2. **Event-driven architecture** is the foundation of Spring Cloud Bus, and it allows systems to stay in sync with each other.

### Example Setup

Let’s set up an example where we use **Spring Cloud Config** to manage configurations and **Spring Cloud Bus** to propagate changes across microservices.

#### Steps:

1. **Set up Spring Cloud Config Server**
2. **Set up Spring Cloud Config Client**
3. **Set up Spring Cloud Bus with a Message Broker (RabbitMQ)**
4. **Trigger a Config Change and Propagate it using Spring Cloud Bus**

### Step-by-Step Implementation

#### 1. Set up Spring Cloud Config Server
First, we need a config server to serve configuration properties. 

Add dependencies in your `pom.xml` or `build.gradle` for Spring Cloud Config Server:

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-config</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-bus-amqp</artifactId> <!-- For RabbitMQ Bus -->
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-amqp</artifactId> <!-- RabbitMQ -->
</dependency>
```

Then, create a Spring Boot application class for the config server:

```
@SpringBootApplication
@EnableConfigServer
public class ConfigServerApplication {
    public static void main(String[] args) {
        SpringApplication.run(ConfigServerApplication.class, args);
    }
}
```

### Set up Spring Cloud Bus with RabbitMQ
Make sure RabbitMQ is running, or use any other supported message broker like Kafka.

Here’s the setup for RabbitMQ in application.yml:

```
spring:
  rabbitmq:
    host: localhost
    port: 5672
    username: guest
    password: guest
```

### Propagate Configuration Changes
Now, whenever you update a configuration in the config server (e.g., a property value in the Git repository), the Spring Cloud Bus will broadcast the change to the client applications.

To trigger a refresh event from the config server to the clients, you can publish an event like this:

```
@Autowired
private Environment environment;

@Autowired
private ApplicationEventPublisher publisher;

@RequestMapping("/refresh")
public String refresh() {
    publisher.publishEvent(new RefreshRemoteApplicationEvent(this, null,
                                  environment.getProperty("spring.application.name")));
    return "Config refresh triggered!";
}
```

You can also send a refresh signal from the config server by calling the /actuator/bus-refresh endpoint, which triggers the refresh event across all clients. For example:

```
curl -X POST http://localhost:8888/actuator/bus-refresh
```

#### Result
When a configuration property is updated in the Git repository, it will automatically be propagated to all connected client services using the Spring Cloud Bus with RabbitMQ or Kafka.

#### Key Points:
Spring Cloud Config manages and serves the configuration.
Spring Cloud Bus uses RabbitMQ or Kafka to propagate changes to the clients.
Event-driven model allows microservices to dynamically react to configuration changes, reducing downtime and manual interventions.

#### Conclusion
Spring Cloud Bus provides a seamless way to propagate configuration changes across distributed systems. When integrated with Spring Cloud Config, it can ensure that your microservices remain in sync with the latest configuration.

<img width="1295" alt="image" src="https://github.com/user-attachments/assets/51fc12ab-7993-4ec2-8de1-304ccad849aa" />

















