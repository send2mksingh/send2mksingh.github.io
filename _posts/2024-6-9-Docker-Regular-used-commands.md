---
 layout: post
 title: Docker regular used commands
---

Certainly! Here is a comprehensive list of Docker commands with examples covering various aspects of Docker usage, including container management, image management, networking, volumes, and more.

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

These commands and examples should cover a wide range of Docker functionalities. For more details on each command and its options, you can use the Docker documentation or the `--help` flag with any Docker command.