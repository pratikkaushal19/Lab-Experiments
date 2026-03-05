# 27-01-2026

## Topic: Docker Installation on macOS

### Objective
To install Docker on macOS and verify the installation using terminal commands.

---

## Steps Performed

### 1. Installing Docker using Homebrew
Homebrew was used to install Docker on macOS.

```bash
brew install docker
```

### 2. Verifying Docker Installation

After installation, Docker version was checked to confirm successful setup.

```bash
docker --version
```
Output shows that Docker was installed successfully.

### 3. Downloading Docker Desktop for Mac

Docker Desktop was downloaded for macOS using the following command:

```bash
curl -L https://desktop.docker.com/mac/main/arm64/Docker.dmg -o Docker.dmg
```
This downloads the Docker Desktop installer file.

## Screenshots

### Docker Installation
![](./images/image1.jpeg)