#  Docker Compose 
 **Date:** 25.02.2026  

---

##  Aim

To understand the difference between `docker run` and `docker compose` by deploying an Nginx container using Docker Compose and verifying container lifecycle operations.

---

## Step 1: Create Project Directory

```bash
mkdir docker-test
cd docker-test
```
![](./images/image1.jpeg)

## Step 2: Create docker-compose.yml File
```bash
touch docker-compose.yml
```

Open the file and add the following content:

```bash
version: '3.8'

services:
  nginx:
    image: nginx:alpine
    container_name: my-nginx
    ports:
      - "8080:80"
    volumes:
      - ./html:/usr/share/nginx/html
    environment:
      - NGINX_HOST=localhost
    restart: unless-stopped
```
![](./images/image2.jpeg)

## Step 3: Run Docker Compose
```bash
docker compose up -d
```
Observation: 
Image pulled successfully

Container created successfully
![](./images/image3.jpeg)

## Step 4: Verify Running Container
```bash
docker ps
```
Observation:

Container my-nginx is running

Port mapping 8080 -> 80 confirmed

![](./images/image4.jpeg)

## Step 5: Check Container Logs
```bash
docker compose logs
```
Observation:

Nginx configuration completed

Worker processes started

No errors detected

![](./images/image5.jpeg)

## Step 6: Stop and Remove Container
```bash
docker compose down
```

Observation:

Container removed

Network removed successfully
![](./images/image6.jpeg)

## Step 7: Verify Container Removal
```bash
docker ps
docker ps -a
```
Observation

No running containers

No stopped containers remaining
![](./images/image7.jpeg)

## Step 8: Additional Verification
```bash
docker-compose ps
```
Observation

No services running

Confirms complete cleanup

![](./images/image8.jpeg)

## Key Observations

Docker Compose automatically creates a default network.

The version: '3.8' attribute generates a warning but does not affect execution.

Port mapping works correctly (8080:80).

Container lifecycle management is simplified using:

docker compose up -d

docker compose down

docker compose logs

docker compose ps

## Docker Run vs Docker Compose Comparison
Docker Run	Docker Compose
Imperative approach	Declarative approach
Command-based execution	YAML configuration-based
Suitable for single container	Suitable for multi-container applications
Manual lifecycle management	Simplified lifecycle management
## Result

The Nginx container was successfully deployed using Docker Compose.
The container lifecycle was verified using Docker commands.
The experiment demonstrates that Docker Compose provides a structured and declarative method for managing containers compared to docker run.