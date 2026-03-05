# Docker Volume – Data Persistence

## Aim

To understand how Docker volumes work and how they help in persisting data even after a container is removed.

---

## Step 1: Create Docker Volume

Command:

docker volume create myvolume

---
Output:
![](./images/image1.jpeg)
## Step 2: List Docker Volumes

Command:

docker volume ls

This command shows all the volumes present in Docker.

---
Output:
![](./images/image2.jpeg)
## Step 3: Run Container with Volume

Command:

docker run -it -v myvolume:/data ubuntu bash

This command starts an Ubuntu container and mounts the Docker volume **myvolume** to the **/data** directory inside the container.

---
Output:
![](./images/image3.jpeg)

## Step 4: Create File in Volume

Commands:

cd /data
touch testfile.txt
ls

A file named **testfile.txt** is created inside the mounted volume.

---

## Step 5: Exit Container

Command:

exit

This exits the running container.

---

## Step 6: Run Another Container and Check Data

Command:

docker run -it -v myvolume:/data ubuntu bash

Then run:

cd /data
ls

If **testfile.txt** is visible, it means the data is stored in the Docker volume and persists even after the container is stopped.

---
Output:
![](./images/image4.jpeg)


## Conclusion

Docker volumes provide persistent storage.
They allow data to remain safe even when containers are removed or recreated.


Output:
![](./images/image4.jpeg)