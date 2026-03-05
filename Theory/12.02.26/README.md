# Docker Mounts Lab – Bind Mount and tmpfs Mount (macOS)

**Date:** 12.02.26  
**Platform:** macOS (Docker Desktop)  
**Objective:** To perform Bind Mount and tmpfs Mount tasks using Docker.

---

## Task 1: Create Bind Mount 

### Step 1: Create a folder on host machine

```bash
mkdir -p ~/html
```

### Step 2: Create a sample HTML file
```bash
echo "<h1>Hello from Mac Bind Mount</h1>" > ~/html/index.htm
```

### Method 1: Using -v
```bash
docker run -d \
  --name nginx-container \
  -v ~/html:/usr/share/nginx/html \
  -p 8080:80 \
  nginx
  ```
![](./images/image1.jpeg)
### Method 2: Using --mount
```bash
docker run -d \
  --name nginx-container \
  --mount type=bind,source=$HOME/html,target=/usr/share/nginx/html \
  -p 8080:80 \
  nginx
  ```
![](./images/image2.jpeg)
## Observation

Files edited on the host system reflect immediately inside the container.

Bind mount allows live synchronization between host and container.
![](./images/image3.jpeg)

## Task 2: Remove Bind Mount

Bind mount does not require separate deletion.
It is removed automatically when the container is removed.

### Remove the container
```bash
docker rm -f nginx-container
```
![](./images/image4.jpeg)

## Task 3: Create tmpfs Mount (Temporary Storage)

tmpfs mount stores data in memory (RAM) and is removed when the container stops.

### Using --tmpfs
```bash
docker run -d \
--name temp-container \
--tmpfs /app/cache \
nginx
```
![](./images/image5.jpeg)

### Verification (Inside Container)
```bash
docker exec -it temp-container sh
df -h | grep tmpfs
```
![](./images/image5.jpeg)

### Remove tmpfs Container
```bash
docker rm -f temp-container
```
![](./images/image6.jpeg)

## Conclusion

Bind mounts connect host directories directly to  containers.

Changes on host reflect instantly inside the container.

tmpfs mounts provide temporary in-memory storage and disappear after container removal.