---
 layout: post
 title: Docker regular used commands
---

To create a Docker container without running it, you can use the `docker create` command. This command sets up the container from an image but does not start it. Here is the syntax and an example of how to use the command:

### Command Syntax
```bash
docker create [OPTIONS] IMAGE [COMMAND] [ARG...]
```

### Example

1. **Pull an Image** (optional if the image is not already available locally):
   ```bash
   docker pull nginx
   ```

2. **Create a Container**:
   ```bash
   docker create --name my_nginx_container nginx
   ```

### Explanation

- `docker create`: The command to create a new container.
- `--name my_nginx_container`: Optionally provide a name for the container.
- `nginx`: The name of the image to create the container from.

This command will output a long string which is the container ID.

### Verify the Container Creation

To verify that the container has been created but not started, you can list all containers, including the ones that are not running:

```bash
docker ps -a
```

This will display all containers, and you should see your newly created container in the list with the `Created` status, indicating that it has been created but not started.


### Docker Container Management

1. **Run a container**
   - **Command**:
     ```bash
     docker run -d --name my-container nginx
     ```
   - **Example**: Runs an `nginx` container in detached mode.

2. **List running containers**
   - **Command**:
     ```bash
     docker ps
     ```
   - **Example**: Lists all currently running containers.

3. **List all containers (running and stopped)**
   - **Command**:
     ```bash
     docker ps -a
     ```
   - **Example**: Lists all containers, including stopped ones.

4. **Stop a container**
   - **Command**:
     ```bash
     docker stop my-container
     ```
   - **Example**: Stops the container named `my-container`.

5. **Start a container**
   - **Command**:
     ```bash
     docker start my-container
     ```
   - **Example**: Starts the container named `my-container`.

6. **Remove a container**
   - **Command**:
     ```bash
     docker rm my-container
     ```
   - **Example**: Removes the container named `my-container`.

7. **View container logs**
   - **Command**:
     ```bash
     docker logs my-container
     ```
   - **Example**: Shows the logs of the container named `my-container`.

8. **Execute a command in a running container**
   - **Command**:
     ```bash
     docker exec -it my-container /bin/bash
     ```
   - **Example**: Opens an interactive shell in the container named `my-container`.

### Docker Image Management

1. **List images**
   - **Command**:
     ```bash
     docker images
     ```
   - **Example**: Lists all Docker images on the host.

2. **Pull an image from Docker Hub**
   - **Command**:
     ```bash
     docker pull nginx
     ```
   - **Example**: Pulls the `nginx` image from Docker Hub.

3. **Build an image from a Dockerfile**
   - **Command**:
     ```bash
     docker build -t my-image .
     ```
   - **Example**: Builds an image named `my-image` from the Dockerfile in the current directory.

4. **Remove an image**
   - **Command**:
     ```bash
     docker rmi my-image
     ```
   - **Example**: Removes the image named `my-image`.

5. **Tag an image**
   - **Command**:
     ```bash
     docker tag my-image my-repo/my-image:latest
     ```
   - **Example**: Tags `my-image` with `my-repo/my-image:latest`.

6. **Push an image to Docker Hub**
   - **Command**:
     ```bash
     docker push my-repo/my-image:latest
     ```
   - **Example**: Pushes the image `my-repo/my-image:latest` to Docker Hub.

### Docker Networking

1. **List networks**
   - **Command**:
     ```bash
     docker network ls
     ```
   - **Example**: Lists all Docker networks.

2. **Create a network**
   - **Command**:
     ```bash
     docker network create my-network
     ```
   - **Example**: Creates a network named `my-network`.

3. **Connect a container to a network**
   - **Command**:
     ```bash
     docker network connect my-network my-container
     ```
   - **Example**: Connects the container named `my-container` to the network `my-network`.

4. **Disconnect a container from a network**
   - **Command**:
     ```bash
     docker network disconnect my-network my-container
     ```
   - **Example**: Disconnects the container named `my-container` from the network `my-network`.

5. **Remove a network**
   - **Command**:
     ```bash
     docker network rm my-network
     ```
   - **Example**: Removes the network named `my-network`.

### Docker Volumes

1. **List volumes**
   - **Command**:
     ```bash
     docker volume ls
     ```
   - **Example**: Lists all Docker volumes.

2. **Create a volume**
   - **Command**:
     ```bash
     docker volume create my-volume
     ```
   - **Example**: Creates a volume named `my-volume`.

3. **Mount a volume to a container**
   - **Command**:
     ```bash
     docker run -d --name my-container -v my-volume:/data nginx
     ```
   - **Example**: Mounts the volume `my-volume` to the `/data` directory inside the `nginx` container.

4. **Inspect a volume**
   - **Command**:
     ```bash
     docker volume inspect my-volume
     ```
   - **Example**: Provides detailed information about the volume named `my-volume`.

5. **Remove a volume**
   - **Command**:
     ```bash
     docker volume rm my-volume
     ```
   - **Example**: Removes the volume named `my-volume`.

### Docker Compose

1. **Start services defined in a docker-compose file**
   - **Command**:
     ```bash
     docker-compose up -d
     ```
   - **Example**: Starts all services defined in the `docker-compose.yml` file in detached mode.

2. **Stop services defined in a docker-compose file**
   - **Command**:
     ```bash
     docker-compose down
     ```
   - **Example**: Stops and removes all services defined in the `docker-compose.yml` file.

3. **View service logs**
   - **Command**:
     ```bash
     docker-compose logs
     ```
   - **Example**: Displays logs for all services defined in the `docker-compose.yml` file.

4. **Scale a service**
   - **Command**:
     ```bash
     docker-compose scale web=3
     ```
   - **Example**: Scales the `web` service to 3 instances (deprecated in favor of `docker-compose up --scale`).

### Docker Swarm

1. **Initialize a swarm**
   - **Command**:
     ```bash
     docker swarm init
     ```
   - **Example**: Initializes the current Docker engine as a swarm manager.

2. **Join a swarm as a worker**
   - **Command**:
     ```bash
     docker swarm join --token <token> <manager-ip>:2377
     ```
   - **Example**: Joins an existing swarm as a worker node using the provided token and manager IP.

3. **List swarm nodes**
   - **Command**:
     ```bash
     docker node ls
     ```
   - **Example**: Lists all nodes in the swarm.

4. **Deploy a stack to the swarm**
   - **Command**:
     ```bash
     docker stack deploy -c docker-compose.yml my-stack
     ```
   - **Example**: Deploys a stack named `my-stack` using the `docker-compose.yml` file.

5. **Remove a stack from the swarm**
   - **Command**:
     ```bash
     docker stack rm my-stack
     ```
   - **Example**: Removes the stack named `my-stack` from the swarm.



The `docker diff` command shows changes made to the filesystem of a Docker container. Here’s a step-by-step example:

1. **Start a Docker container:**

   ```bash
   docker run -d --name mycontainer ubuntu:latest
   ```

   This command runs a container named `mycontainer` using the latest Ubuntu image.

2. **Make some changes inside the container:**

   ```bash
   docker exec mycontainer bash -c "echo 'Hello, Docker!' > /root/hello.txt"
   ```

   This command creates a file `/root/hello.txt` inside the `mycontainer` container.

3. **Use the `docker diff` command to see the changes:**

   ```bash
   docker diff mycontainer
   ```

   The output might look something like this:

   ```
   A /root
   A /root/hello.txt
   ```

   This indicates that a new file (`hello.txt`) has been added to the `/root` directory.

4. **Stop and remove the container (optional):**

   ```bash
   docker stop mycontainer
   docker rm mycontainer
   ```

Here’s a summary of the commands:

```bash
docker run -d --name mycontainer ubuntu:latest
docker exec mycontainer bash -c "echo 'Hello, Docker!' > /root/hello.txt"
docker diff mycontainer
docker stop mycontainer
docker rm mycontainer
```

This example shows how to start a container, make a change to its filesystem, and then use `docker diff` to see the difference.

These commands and examples should cover a wide range of Docker functionalities. For more details on each command and its options, you can use the Docker documentation or the `--help` flag with any Docker command.


Creating an image from a running container involves using the `docker commit` command. Here's how you can do it:

1. **Start a Docker container (if not already running):**

   ```bash
   docker run -d --name mycontainer ubuntu:latest
   ```

2. **Make some changes inside the container:**

   ```bash
   docker exec mycontainer bash -c "echo 'Hello, Docker!' > /root/hello.txt"
   ```

3. **Create an image from the running container:**

   ```bash
   docker commit mycontainer mynewimage:latest
   ```

   This command commits the changes made in the container `mycontainer` to a new image named `mynewimage` with the tag `latest`.

4. **Verify the new image:**

   ```bash
   docker images
   ```

   You should see `mynewimage` listed among the available images.

Here’s a summary of the commands:

```bash
docker run -d --name mycontainer ubuntu:latest
docker exec mycontainer bash -c "echo 'Hello, Docker!' > /root/hello.txt"
docker commit mycontainer mynewimage:latest
docker images
```

This process captures the current state of a container and saves it as a new Docker image.



The command `docker container inspect volumename` is not correct for inspecting volumes. To inspect a volume, you should use the `docker volume inspect` command. Here’s how to inspect a Docker volume:

1. **List all volumes to get the volume name (if you don't already know it):**

   ```bash
   docker volume ls
   ```

2. **Inspect a specific volume:**

   ```bash
   docker volume inspect volumename
   ```

Replace `volumename` with the actual name of the volume you want to inspect.

Here's an example:

```bash
docker volume ls
docker volume inspect myvolume
```

The `docker volume inspect myvolume` command will provide detailed information about the volume named `myvolume`, including its mount point and configuration options.


To inspect a Docker container, you should use the `docker container inspect` command. Here’s how you can do it:

1. **List all running containers to get the container ID or name:**

   ```bash
   docker ps
   ```

2. **Inspect a specific container:**

   ```bash
   docker container inspect containername_or_id
   ```

Replace `containername_or_id` with the actual name or ID of the container you want to inspect.

Here’s an example:

1. **List all running containers:**

   ```bash
   docker ps
   ```

   This will provide output similar to:

   ```
   CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS         PORTS     NAMES
   abc123def456   ubuntu:latest  "/bin/bash"              10 minutes ago  Up 10 minutes            mycontainer
   ```

2. **Inspect the container named `mycontainer`:**

   ```bash
   docker container inspect mycontainer
   ```

This command will display detailed information about the container, including its configuration, network settings, and other metadata.



Volume host to container ------------------------------------------------------------------------------------------------

Verify files in /home/ec2-user

docker run -it --name hostcont -v  /home/ec2-user:/manoj-dir --privileged=true ubuntu  /bin/bash

cd /manoj-dir



--------Now try to create volume using command ------
docker run -it --name container3 -v /volume2   ubuntu /bin/bash

do ls - cd /volume
now create one file cont3file and exit

----now create one more container, and share volume2

---> docker run -it --name Container4 --privileged=true --volume-from Container 3 ubuntu  /bin/bash

-- -- now you are inside Container, do ls, you can see volume2


To create a Docker container with a specific network, you can use the `--network` option in the `docker run` command. This option allows you to specify the network that the container will connect to.

Here are the steps to create a container with a specific network:

### Step 1: Create a Docker Network (if not already created)
First, create a Docker network using the `docker network create` command. Docker supports different network drivers, such as `bridge`, `overlay`, and `host`. For this example, we'll create a custom bridge network.

```bash
docker network create my_custom_network
```

### Step 2: Run the Docker Container with the Specific Network
Next, use the `--network` option to run a container connected to the `my_custom_network` network.

```bash
docker run -it --name my_container --network my_custom_network centos /bin/bash
```

This command creates a new container named `my_container` using the CentOS image and connects it to the `my_custom_network` network.

### Example Commands

#### Creating a Custom Bridge Network
```bash
docker network create my_custom_network
```

#### Running a New Container in the Custom Network
```bash
docker run -it --name my_container --network my_custom_network centos /bin/bash
```

### Additional Examples with Different Network Drivers

#### Creating an Overlay Network
Overlay networks are typically used in Docker Swarm mode.
```bash
docker network create -d overlay my_overlay_network
```

#### Creating a Host Network
Using the host network mode provides the container with direct access to the host’s network interfaces.
```bash
docker run -it --name my_container --network host centos /bin/bash
```

### Checking Network Connections

You can verify which network a container is connected to using the `docker network inspect` command.

#### Inspecting the Network
```bash
docker network inspect my_custom_network
```

This command provides detailed information about the network, including the containers connected to it.

### Running `ping` in the Container

After the container is running with the specific network, you can install `ping` and use it as needed.

#### Accessing the Container’s Shell
```bash
docker exec -it my_container /bin/bash
```

#### Installing `ping` (if necessary)
```bash
yum update -y
yum install -y iputils
```

#### Running the `ping` Command
```bash
ping 8.8.8.8
```

### Summary

By following these steps, you can create and run a Docker container with a specific network. This setup is useful for network isolation, segmentation, and custom network configurations within your Docker environment.