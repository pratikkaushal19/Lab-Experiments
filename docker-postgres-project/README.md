# Containerized Web Application with PostgreSQL using Docker Compose and Macvlan

## Project Overview

This project demonstrates how to design, containerize, and deploy a backend web application connected to a PostgreSQL database using Docker. The application is orchestrated using Docker Compose and uses Macvlan networking to assign static IP addresses to containers.

The system demonstrates:

- Multi-stage Docker image builds
- Container networking using Macvlan
- Persistent storage using Docker volumes
- Service orchestration using Docker Compose
- Backend API interacting with PostgreSQL

---

# Technology Stack

| Component | Technology |
|-----------|------------|
| Backend API | FastAPI (Python) |
| Database | PostgreSQL |
| Containerization | Docker |
| Orchestration | Docker Compose |
| Networking | Macvlan |
| Volume | Docker Named Volume |

---

# Project Architecture
# Containerized Web Application with PostgreSQL using Docker Compose and Macvlan

## Project Overview

This project demonstrates how to design, containerize, and deploy a backend web application connected to a PostgreSQL database using Docker. The application is orchestrated using Docker Compose and uses Macvlan networking to assign static IP addresses to containers.

The system demonstrates:

- Multi-stage Docker image builds
- Container networking using Macvlan
- Persistent storage using Docker volumes
- Service orchestration using Docker Compose
- Backend API interacting with PostgreSQL

---

# Technology Stack

| Component | Technology |
|-----------|------------|
| Backend API | FastAPI (Python) |
| Database | PostgreSQL |
| Containerization | Docker |
| Orchestration | Docker Compose |
| Networking | Macvlan |
| Volume | Docker Named Volume |

---

# Project Architecture
Client (Browser/Postman)
|
Backend Container (FastAPI)
IP: 192.168.1.50
|
PostgreSQL Container
IP: 192.168.1.51
|
Docker Named Volume (Persistent Storage)

---

# Project Structure
docker-postgres-project
│
├── backend
│ ├── app.py
│ ├── requirements.txt
│ ├── Dockerfile
│ └── .dockerignore
│
├── database
│ ├── Dockerfile
│ ├── init.sql
│ └── .dockerignore
│
└── docker-compose.yml

---

# Backend API Endpoints

| Method | Endpoint | Description |
|------|------|------|
| GET | `/health` | Health check endpoint |
| POST | `/add?name=value` | Insert record into database |
| GET | `/items` | Fetch all records |

---

# Docker Image Build Strategy

The backend image uses **multi-stage builds** to reduce the final image size.

Steps used:

1. Install dependencies in builder stage
2. Copy only required binaries to runtime stage
3. Use minimal base image (`python:3.11-slim`)
4. Run application using non-root user

Benefits:

- Smaller image size
- Improved security
- Faster deployment

---

# Database Container

A custom PostgreSQL Dockerfile is used instead of the default image.

Environment variables configured:

Database initialization is handled using:



Database initialization is handled using:

which automatically creates the required table at startup.

---

# Networking Configuration (Macvlan)

Macvlan allows containers to appear as physical devices on the local network with their own IP addresses.

Network configuration used:


Containers assigned static IP addresses:
Backend Container → 192.168.1.50
PostgreSQL Container → 192.168.1.51

Create the Macvlan network manually:

```bash
docker network create -d macvlan \
--subnet=192.168.1.0/24 \
--gateway=192.168.1.1 \
mynetwork

![](./images/image1.jpeg)
![](./images/image2.jpeg)
![](./images/image3.jpeg)
![](./images/image4.jpeg)
![](./images/image5.jpeg)
![](./images/image6.jpeg)
![](./images/image7.jpeg)
![](./images/image8.jpeg)



