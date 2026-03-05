# Docker Networking Hands-On 

This hands-on demonstrates Docker networking concepts on macOS, including:

- Inspecting default bridge network
- Creating a custom bridge network
- Running containers in the same network
- Testing container DNS resolution
- Inspecting container network configuration
- Exposing containers using port mapping
- Accessing nginx via browser

---

## Step 1: List Default Docker Networks

```bash
docker network ls
```
![](./images/image1.jpeg)

## Step 2: Inspect Default Bridge Network

```bash
docker network inspect bridge
```
![](./images/image2.jpeg)

## Step 3: Create Custom Bridge Network

```bash
docker network create my_bridge
```

## Step 4: Verify Custom Network

```bash
docker network ls
```
![](./images/image3.jpeg)

## Step 5: Inspect Custom Bridge Network

```bash
docker network inspect my_bridge
```
![](./images/image4.jpeg)

## Step 6: Run Containers in Custom Network
Run Nginx Container

```bash
docker run -dit --name container1 --network my_bridge nginx
```
Run BusyBox Container
```bash
docker run -dit --name container2 --network my_bridge busybox
``` 
Both containers are connected to my_bridge.

![](./images/image5.jpeg)

## Step 7: Test Container Communication (DNS Resolution)
```bash
docker exec -it container2 ping container1
```
![](./images/image6.jpeg)

## Step 8: Inspect Container Network Configuration
```bash
docker inspect container2
```
![](./images/image7.jpeg)

## Step 9: Run Nginx with Port Mapping 
```bash
docker run -d -p 8080:80 --name nginx1 nginx
```
![](./images/image8.jpeg)

## Step 10: Access Nginx in Browser

Open:

```bash
http://localhost:8080
```
![](./images/image9.jpeg)