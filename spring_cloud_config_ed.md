# Encrypt and Decrypt Properties in Spring Boot Cloud Config

## Generate Keystore for Encryption/Decryption:

Before setting up the Config Server, you need a keystore file to handle encryption/decryption. 
<br> You can use keytool (provided by Java) to generate a keystore.

**Example:**
```
keytool -genkeypair -alias configkey -keyalg RSA -keysize 2048
        -keystore config-server.p12 -storetype PKCS12 -validity 3650
```

This command will generate a keystore (config-server.p12) containing a key pair. 
<br> The alias configkey will be used for encryption/decryption.

## Set Up Config Server (application.yml):

In the Config Server, you need to configure encryption using the keystore. 
<br> The application.yml configuration looks like this:

```
spring:
  cloud:
    config:
      server:
        encrypt:
          key-store: classpath:config-server.p12  # Path to keystore
          key-store-password: your-keystore-password
          key-alias: configkey
          key-password: your-key-password

```

-  key-store: Path to the keystore file.
-  key-store-password: Password to the keystore.
-  key-alias: Alias for the key in the keystore.
-  key-password: Password for the key.

## Run Config Server:

Start the Config Server. It will listen for requests to encrypt or decrypt properties.

# Encrypt Sensitive Properties
To encrypt a sensitive property (like a database password or an API key), you can use 
<br> the encrypt endpoint provided by Spring Cloud Config Server.

## Encrypt Property Using REST API:

You can use the curl command or any HTTP client to send a POST request to the Config Server’s encrypt endpoint:

```
curl -X POST http://localhost:8888/encrypt -d 'my-secret-password'
```

The server will return an encrypted value:
```
{cipher}XkQbL7dpZJd8kZJltkN5A==
```

## Store the Encrypted Value:

The encrypted value will look like {cipher}XkQbL7dpZJd8kZJltkN5A==. 
<br> You can store this in your Git repository or file system as the configuration value.

<br> For example, in application.properties or application.yml:

```
my.sensitive.property={cipher}XkQbL7dpZJd8kZJltkN5A==
```

## Set Up Spring Boot Application
Your Spring Boot application needs to retrieve the encrypted property and automatically 
<br> decrypt it using the keys defined in the Config Server.

### Spring Boot Application Configuration (application.yml):

Configure the Spring Boot application to use the Spring Cloud Config Server by adding the following to application.yml:

```
spring:
  cloud:
    config:
      uri: http://localhost:8888
```
This tells your Spring Boot application to connect to the Config Server running on localhost:8888 to retrieve configuration properties.

### Accessing Decrypted Property:

In your Spring Boot application, you can access the decrypted properties as usual. 
<br> For example, you can use @Value to inject the value into a class:

```
@Component
public class MyComponent {

    @Value("${my.sensitive.property}")
    private String sensitiveProperty;

    @PostConstruct
    public void init() {
        System.out.println("Decrypted Property: " + sensitiveProperty);
    }
}
```
<br>
The my.sensitive.property will be automatically decrypted by the Spring Cloud Config Server when your Spring Boot application starts.











