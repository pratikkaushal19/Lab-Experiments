# Docker Daemon Access on macOS

**Date:** 04.02.26

---

## Introduction

Docker is a widely used containerization platform that allows applications to run in isolated environments called containers. The working of Docker depends on the underlying operating system on which it is installed.

On macOS, Docker does not run directly on the host operating system. Instead, Docker Desktop is used, which internally runs Docker inside a lightweight Linux Virtual Machine (VM).

---

## Docker Architecture on macOS

Docker Desktop manages a Linux-based virtual machine where the Docker Engine runs. The Docker CLI installed on macOS communicates with this Docker Engine through a secure mechanism.

On macOS, Docker Desktop runs Docker inside a Linux VM and exposes the Docker API via a Unix domain socket (`/var/run/docker.sock`) instead of TCP port `2375`. Therefore, the Docker API is accessed using `curl` with the Unix socket.

---

## Docker Configuration File

The Docker daemon configuration file is generally located at:

```bash
/etc/docker/daemon.json
```

A sample configuration file is shown below:

```json
{
  "hosts": [
    "unix:///var/run/docker.sock",
    "tcp://0.0.0.0:2375"
  ]
}
```
![](./images/image1.jpeg)

![](./images/image2.jpeg)
### Restarting Docker on macOS

Unlike Linux systems, macOS does not use systemctl to manage services. Docker must be restarted using Docker Desktop.

The following commands are used to restart Docker Desktop from the terminal:

```bash
osascript -e 'quit app "Docker"'
open -a Docker
```


This stops and restarts Docker Desktop, thereby restarting the Docker Engine inside the Linux VM.

![](./images/image3.jpeg)

## Verifying Docker Installation

To verify that Docker is installed and running correctly, the following command is used:
```bash
docker version
```


This command displays both the Docker Client and Docker Server information. Successful output confirms that Docker Desktop and the Docker Engine are running properly.

![](./images/image4.jpeg)
```bash
Docker Unix Socket on macOS
```

Docker Desktop exposes a Unix domain socket that enables communication between the Docker CLI and the Docker Engine.

The socket is located at:
```bash
/var/run/docker.sock
```


To verify the socket, the following command is used:
```bash
ls -l /var/run/docker.sock
```

This confirms the existence and linkage of the Docker socket.



Accessing Docker API Using Unix Socket

Since Docker Desktop on macOS does not expose the Docker API over TCP port 2375, the API is accessed using the Unix socket.

The following command is used to access the Docker API:
```bash
curl --unix-socket /var/run/docker.sock http://docker/version
```


This command returns Docker version information in JSON format, confirming that the Docker API is accessible through the Unix socket.

![](./images/image5.jpeg)


## Conclusion

Docker on macOS operates differently compared to Linux systems. Docker Desktop runs Docker inside a Linux virtual machine and exposes the Docker API through a Unix domain socket rather than a TCP port.

Docker functionality on macOS can be verified using docker version and Unix socket-based curl commands. This approach ensures improved security and stability while working with Docker on macOS.