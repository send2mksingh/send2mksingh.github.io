---
 layout: post
 title: Docker Compose
---

Docker Compose is a tool for defining and running multi-container Docker applications. With Docker Compose, you use a YAML file to configure your application's services, networks, and volumes, making it easy to set up and manage complex applications.

### Step-by-Step Example

Let's create a simple example with two services: a web server (using Nginx) and a Redis database.

### Step 1: Install Docker and Docker Compose

Make sure Docker and Docker Compose are installed on your system. You can find installation instructions [here](https://docs.docker.com/compose/install/).

### Step 2: Create a Project Directory

Create a directory for your project and navigate into it:

```bash
mkdir my_docker_project
cd my_docker_project
```

### Step 3: Create a `docker-compose.yml` File

In your project directory, create a `docker-compose.yml` file. This file will define the services for your application.

```yaml
version: '3.8'

services:
  web:
    image: nginx:latest
    ports:
      - "8080:80"

  redis:
    image: redis:latest
```

This `docker-compose.yml` file does the following:

- Defines two services: `web` and `redis`.
- The `web` service uses the Nginx image and maps port 8080 on the host to port 80 in the container.
- The `redis` service uses the Redis image.

### Step 4: Run Docker Compose

In your project directory, run the following command to start the services:

```bash
docker-compose up
```

This command does the following:

- Pulls the necessary images (`nginx` and `redis`) from Docker Hub if they are not already available locally.
- Creates and starts the containers for both services.
- Streams the logs for the services to your terminal.

### Step 5: Access the Web Service

Open your web browser and go to `http://localhost:8080`. You should see the default Nginx welcome page, indicating that the Nginx container is running and accessible.

### Step 6: Stop the Services

To stop the services, press `Ctrl+C` in the terminal where Docker Compose is running. Alternatively, you can run:

```bash
docker-compose down
```

This command stops and removes the containers, networks, and volumes created by `docker-compose up`.

### Summary

- **Create a project directory**: `mkdir my_docker_project && cd my_docker_project`
- **Create a `docker-compose.yml` file** with service definitions.
- **Run Docker Compose**: `docker-compose up`
- **Access the web service** at `http://localhost:8080`
- **Stop the services**: `Ctrl+C` or `docker-compose down`

This simple example demonstrates how Docker Compose can be used to define and run multi-container applications easily. You can extend this example by adding more services, networks, and volumes as needed for your applications.