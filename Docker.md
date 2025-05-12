# Docker Notes

## What is Docker?

Docker is a platform used to **build**, **package**, **deploy**, and **run** applications in containers.

* It is lightweight and helps with fast and efficient deployments.
* You can pull pre-built Docker images from Docker Hub.

```bash
docker pull <image-name>
```

---

## Running a Docker Container

To build and run a container from an image:

```bash
docker run <image-name>
```

For example, to run a MySQL container:

```bash
docker run --name mysql-container \
  -e MYSQL_USER=Sujana \
  -e MYSQL_PASSWORD=haha \
  -p 1433:1433 \
  -d mysql:latest
```

* `-p 1433:1433` maps host port to container port
* `-e` sets environment variables
* `-d` runs in detached mode

---

## Docker Compose

Docker Compose is a tool for **defining and running multi-container** Docker applications using a `docker-compose.yml` file.

### Example `docker-compose.yml`

```yaml
version: '3.9'

services:
  db:
    image: postgres:15
    container_name: db
    environment:
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=password
      - POSTGRES_DB=mydb
    volumes:
      - db-data:/var/lib/postgresql/data
    networks:
      - app-network

volumes:
  db-data:

networks:
  app-network:
```

### Commands:

```bash
docker compose up -d     # Start containers in detached mode
docker compose down      # Stop and remove containers, networks, volumes
```

---

## Dockerfile

A `Dockerfile` is used to create **custom Docker images** for your applications.

### Typical Project Structure:

```
Application/
├── app.py
├── Dockerfile
└── requirements.txt
```

### Example `Dockerfile`

```Dockerfile
FROM python:latest
WORKDIR /application
COPY . .
RUN pip install -r requirements.txt
CMD ["python", "app.py"]
```

### Build and Run

```bash
docker build -t my-python-app:latest .
docker run -p 8080:8080 my-python-app:latest
```

---

## Common Docker Commands

```bash
docker pull <image-name>        # Pull image from Docker Hub
docker images                   # List downloaded images
docker ps                       # List running containers
docker ps -a                    # List all containers (including stopped)
docker run <image-name>         # Run a container
docker run -it <image-name>     # Run interactively
docker start <container>        # Start existing container
docker stop <container>         # Stop running container
docker rm <container-id>        # Remove container
docker rmi <image-name>         # Remove image
```

### More examples:

```bash
docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql

docker run --name anyname -e MYSQL_ROOT_PASSWORD=my-secret-pw -p 3306:8080 -d mysql

docker exec -it <container-name> /bin/bash    # Access running container shell

docker network ls                              # List networks
docker network create <name>                  # Create a new network

docker compose -f filename.yaml up -d         # Run services using a custom compose file
docker compose -f filename.yaml down          # Tear down the services
```

---

### Summary

* Use **Docker** to build and run containers
* Use **Docker Compose** to manage multi-container applications
* Use **Dockerfile** to define custom images

This guide gives you practical commands and structures for real-world usage and interviews.

