# Containerising a Python Application using Docker (No Source Inside Image)



## Application Code (`app.py`)

```python
# Simple program to verify SAP ID
# Focus of this task is containerization, not Python

import numpy as np   # dependency for learning purpose

stored_sapid = "500120492"

user_sapid = input("Enter your SAP ID: ")

if user_sapid == stored_sapid:
    print("Matched")
else:
    print("Not Matched")
```

## Dockerfile

This Dockerfile installs Python and NumPy but does not copy the source code into the image. 
```bash
FROM python:3.10-slim

WORKDIR /app

RUN pip install numpy

CMD ["python", "app.py"]

```
![](./images/image1.jpeg)

## Build the image using:

```bash
docker build -t sapid-checkernosrc:1.1 -f nosrc.Dockerfile .

``` 
![](./images/image2.jpeg)

## Verify Image

To confirm the image is created successfully:
```bash
docker images
```

Output:
![](./images/image3.jpeg)

## Run & Test Instructions

Since the source code is not copied into the image, we mount the local folder into the container using volume binding:

```bash
docker run -it -v $(pwd):/app sapid-checkernosrc:1.1
```

Output:

![](./images/image4.jpeg)
## Verify Containers

To view all containers (including stopped):
```bash
docker ps -a
```
![](./images/image5.jpeg)

## Conclusion

This experiment successfully demonstrates:

-Using an official Python base image

-Installing dependencies (NumPy) inside the container

-Building an image without embedding source code

-Running the application using volume mounting

-Testing the container interactively