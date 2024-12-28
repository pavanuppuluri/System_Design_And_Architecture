# Encrypt and Decrypt Properties in Spring Boot Cloud Config

In Spring Cloud Config, you can **encrypt** and **decrypt** sensitive properties (such as passwords, API keys, and other sensitive data) using a **symmetric encryption** algorithm. The most common encryption/decryption approach is to use **JCE (Java Cryptography Extension)** or a **KMS (Key Management Service)** like **AWS KMS** or **HashiCorp Vault**.

Here’s how you can encrypt and decrypt properties in **Spring Boot** with **Spring Cloud Config**:

## 1. Using Spring Cloud Config Server with Encryption/Decryption

### Encrypting a Property

In Spring Cloud Config, encryption can be done by using the `encrypt` command from the `Spring Cloud Config` client. Here’s how to encrypt a value:

#### Example:
```bash
$ curl http://localhost:8888/encrypt -d 'mySecretPassword'
```

This will return an encrypted value that can be stored in the configuration file. For example, if your password is mySecretPassword, the result might look like:

```{cipher}Xyz123EncryptedValue```

You can then store the encrypted value in your configuration files, like application.yml or application.properties.

### Decrypting a Property

The Spring Cloud Config Server will automatically decrypt encrypted properties when requested. For example, if the client sends an encrypted property in the request, the server will decrypt it.

If you store an encrypted value in a file like:

yaml
Copy code
myapp:
  secret: '{cipher}Xyz123EncryptedValue'
When the Config Server serves this configuration, it will automatically decrypt the property and return the original value (e.g., mySecretPassword) to the application.
