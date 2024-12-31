# Docker Bridge Example

A **Docker bridge** is a network driver that allows containers to communicate with each other and with the external network while keeping them isolated. By default, Docker uses the **bridge network** when a container is created without any explicit network settings.

## Steps to Create and Use a Docker Bridge Network

### 1. **Create a Custom Bridge Network**

By default, Docker creates a `bridge` network, but you can create a custom bridge network for better isolation and management.

```bash
docker network create --driver bridge my_custom_bridge
```

This command creates a custom bridge network named `my_custom_bridge`.

### 2. **Run Containers on the Custom Bridge Network**

Now, let’s create and run two containers on the custom bridge network. We'll use the `nginx` image for one container and the `redis` image for another.

- **Run the `nginx` container**:

    ```bash
    docker run -d --name my_nginx --network my_custom_bridge nginx
    ```

- **Run the `redis` container**:

    ```bash
    docker run -d --name my_redis --network my_custom_bridge redis
    ```

Both containers (`nginx` and `redis`) are now part of the `my_custom_bridge` network.

### 3. **Verify the Network**

You can check the list of networks to confirm that the custom network was created.

```bash
docker network ls
```

To see more details about your custom bridge network (including connected containers), you can use:

```bash
docker network inspect my_custom_bridge
```

### 4. **Test Container Communication**

With both containers on the same custom bridge network, they can communicate with each other using their container names. For example, let's test the connection from `my_nginx` container to `my_redis` container.

- **Access the `nginx` container**:

    ```bash
    docker exec -it my_nginx /bin/bash
    ```

- **Ping the `redis` container**:

Once inside the `nginx` container, you can ping the `redis` container using its container name (`my_redis`).

```bash
ping my_redis
```

This should return successful ping responses, indicating that the containers can communicate with each other via the custom bridge network.

### 5. **Accessing the Containers Externally**

If you want to access the `nginx` container from your local machine (external network), you need to map its ports when starting the container.

For example, when starting the `nginx` container, you can map the internal port `80` to an external port `8080` on your host machine:

```bash
docker run -d --name my_nginx --network my_custom_bridge -p 8080:80 nginx
```

Now, you can access the `nginx` container by visiting `http://localhost:8080` in your browser.

### 6. **Disconnect a Container from the Network**

If you want to disconnect a container from the network, you can do so with the following command:

```bash
docker network disconnect my_custom_bridge my_nginx
```

This will disconnect the `my_nginx` container from the `my_custom_bridge` network.

### 7. **Remove the Custom Bridge Network**

Once you are done, you can remove the custom bridge network. However, make sure that no containers are attached to it before removing it:

```bash
docker network rm my_custom_bridge
```

## Conclusion:

In this example:
- We created a custom bridge network called `my_custom_bridge`.
- We ran two containers (`nginx` and `redis`) on this custom bridge network.
- We verified the ability of the containers to communicate with each other via their container names.
- We demonstrated how to expose one of the containers to the external network.

This demonstrates the basic use of Docker’s bridge network driver to isolate and connect containers.

## Note

All the microservices that are launched within the same network can communicate with each other using service name


