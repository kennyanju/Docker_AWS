
# Docker Competency Tasks for Enterprise Projects

This tutorial is designed to guide new engineers through mastering essential Docker tasks within the AWS Cloud environment. Completing these tasks will help you become competent in using Docker for enterprise projects.

## 1. Install Docker

Install Docker on an AWS EC2 instance running Amazon Linux 2.

```bash
sudo yum update -y
sudo amazon-linux-extras install docker
sudo service docker start
sudo usermod -a -G docker ec2-user
```

Log out and log back in to ensure Docker can be run without sudo.

---

## 2. Manage Docker Images

Learn how to find, pull, list, and remove Docker images.

```bash
# Pull an image from Docker Hub
docker pull nginx

# List all local images
docker images

# Remove an image
docker rmi nginx
```

---

## 3. Run Containers

Run a container from the nginx image, expose it on port 80.

### Script

```bash
docker run --name my-nginx -d -p 80:80 nginx
```

---

## 4. Build Images with Dockerfile

Create a Dockerfile for a simple web application and build an image from it.

### Dockerfile Example

```Dockerfile
FROM nginx:alpine
COPY . /usr/share/nginx/html
```

### Script to Build Image

```bash
docker build -t my-web-app .
```

---

## 5. Manage Container Data

Learn to use volumes for data persistence.

```bash
# Create a volume
docker volume create my-volume

# Run a container with the volume attached
docker run -d --name devtest -v my-volume:/app nginx:latest
```

---

## 6. Docker Networking

Create a custom network and connect two containers.

```bash
# Create a network
docker network create my-network

# Run two containers and connect them to the network
docker run -d --name nginx --network my-network nginx
docker run -d --name my-app --network my-network my-web-app
```

---

## 7. Docker Compose

Use Docker Compose to define and run a multi-container application.

### docker-compose.yml Example

```yaml
version: '3'
services:
  web:
    image: nginx
    ports:
      - "80:80"
  app:
    image: my-web-app
    depends_on:
      - web
```

### Script to Start Application

```bash
docker-compose up -d
```

---

## 8. Security Practices

Use Docker Bench for Security to assess configurations

Install Docker Bench for Security

```bash
git clone https://github.com/docker/docker-bench-security.git
cd docker-bench-security
sudo sh docker-bench-security.sh
```

Run Docker Bench for Security

```bash
sudo ./docker-bench-security.sh
```

review results, analyse findings and implement reccomendations

---

## 9. Logging and Monitoring

Monitor containers and collect logs.

```bash
# View logs of a container
docker logs my-nginx

# Monitor container metrics
docker stats
```

---

## 10. CI/CD Integration

Integrate Docker with a CI/CD pipeline

- Build Docker image
- Push the image to AWS ECR
- Deploy the container to AWS ECS.

---