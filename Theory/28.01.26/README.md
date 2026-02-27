# 28-01-2026

## Topic: Creating and Running a Java Application using Docker

---

## Objective
To create a Dockerfile for a Java application, build a Docker image, run a container, and verify the output using Docker commands.

---

## Files Used

### Hello.java
A simple Java program used to test Dockerfile automation.

```java
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello from Dockerfile automation");
    }
}
Dockerfile
Dockerfile used to create a Docker image for the Java application.

FROM ubuntu:22.04

RUN apt update && apt install -y openjdk-17-jdk

WORKDIR /home/app

COPY Hello.java .

RUN javac Hello.java

CMD ["java", "Hello"]
```

Steps Performed
### 1. Listing Files in Directory
To verify that Hello.java and Dockerfile are present:

ls

### 2. Building Docker Image
Docker image was built using the following command:

docker build -t java-hello .
This command creates a Docker image named java-hello using the Dockerfile.


### 3. Running Docker Container
The Docker container was run using:

docker run java-hello
Output:

Hello from Dockerfile automation
This confirms that the Java program executed successfully inside the container.

### 4. Listing Docker Images
To view all available Docker images:

docker images
The output shows the java-hello image along with the base ubuntu image.

## Screenshots

### Dockerfile
![Dockerfile](./image1/dockerfile.jpeg)

### Java Program
![Hello Java](./image2/hello-java.jpeg)

### Building Docker Image
![Docker Build](./image3/docker-build.jpeg)

### Running Container and Listing Images
![Docker Run](./image4/docker-run-and-images.jpeg)
![Docker Run](./image5/docker-run-and-images.jpeg)
![Docker Run](./image6/docker-run-and-images.jpeg)