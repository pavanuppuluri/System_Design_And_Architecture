# Spring Cloud Config
<br>
<br>
<img width="897" alt="image" src="https://github.com/user-attachments/assets/e8a063e6-71c5-4aff-bcc6-f7927665c2ef" />

# 9 Ways to Read Configuration Data in Spring Cloud Config Server

## 1. Git Repositories

Spring Cloud Config Server can fetch configuration files from a Git repository, allowing versioned management of configurations.

### Example Configuration:

```yaml
spring:
  cloud:
    config:
      server:
        git:
          uri: https://github.com/myorg/myconfigrepo
          searchPaths: config
          cloneOnStart: true
          username: myusername
          password: mypassword
```

## 2. File System (Local Files)

Configuration can be served from a local file system directory on the Config Server.

### Example Configuration:

```yaml
spring:
  cloud:
    config:
      server:
        native:
          searchLocations: file:/path/to/config/directory/

```
## 3. HashiCorp Vault

Spring Cloud Config Server can integrate with HashiCorp Vault for storing and fetching sensitive configuration data securely.

### Example Configuration:

```yaml
spring:
  cloud:
    config:
      server:
        vault:
          uri: https://vault.example.com
          token: myVaultToken
          backend: secret
          default-context: application

```
## 4. JDBC (Database-backed Configuration)

Configuration can be fetched dynamically from a relational database via JDBC.

### Example Configuration:

```yaml
spring:
  cloud:
    config:
      server:
        jdbc:
          driverClassName: com.mysql.cj.jdbc.Driver
          url: jdbc:mysql://localhost:3306/config_db
          user: dbuser
          password: dbpassword
          sql: SELECT config_value FROM config_table WHERE application = ? AND profile = ?


```
## 5. AWS S3 (Amazon Simple Storage Service)

Spring Cloud Config Server can read configuration files stored in an S3 bucket.

### Example Configuration:

```yaml
spring:
  cloud:
    config:
      server:
        aws:
          s3:
            bucket: my-config-bucket
            region: us-east-1
            accessKey: myAccessKey
            secretKey: mySecretKey


```
## 6. Consul

Consul can be used as a backend for managing configuration in Spring Cloud Config Server.

### Example Configuration:

```yaml
spring:
  cloud:
    config:
      server:
        consul:
          host: localhost
          port: 8500
          scheme: http
          defaultContext: application


```
## 7. Zookeeper

Zookeeper can also be used as a backend to store and serve configuration data.

### Example Configuration:

```yaml
spring:
  cloud:
    config:
      server:
        zookeeper:
          connect-string: localhost:2181

```
## 8. Custom Configuration Backend

You can implement your own custom backend by extending EnvironmentRepository to fetch configuration from any system.

**Example:**
Implement a custom EnvironmentRepository and configure it for use with Spring Cloud Config Server.

**Benefits:**
Highly flexible and customizable for specific use cases.
Allows integration with non-standard configuration sources.

## 9. Classpath (Classpath Resource)

Configuration can be served from files bundled in the application’s classpath (e.g., inside JAR/WAR files or local directories).

### Example Configuration:

```yaml
spring:
  cloud:
    config:
      server:
        native:
          searchLocations: classpath:/config

```

### Summary of the 9 Ways:
1. **Git Repositories**: Fetch from a Git repo, supports version control.
2. **File System (Local Files)**: Read from local directories.
3. **HashiCorp Vault**: Secure and centralized secrets management.
4. **JDBC (Database-backed Configuration)**: Store in a relational database.
5. **AWS S3**: Read from AWS S3 buckets.
6. **Consul**: Use HashiCorp Consul for configuration management.
7. **Zookeeper**: Use Apache Zookeeper for distributed configuration.
8. **Custom Backend**: Implement your own backend using `EnvironmentRepository`.
9. **Classpath**: Read from files bundled in the application’s classpath.

**Note**
Native profile will be used when we are using File System / Classpath way
