# Docker Hello World Spring Boot

A minimal **Spring Boot** sample application for **Docker** and **[Nife.io](https://nife.io)** deployments.

This repository provides a simple "Hello World" Java application that can be built with Docker, run locally, and deployed as a lightweight sample project on [Nife.io](https://nife.io). It is intended as a practical reference for testing containerized Spring Boot deployments and basic platform onboarding.[1] [2] [3]

## Overview

This project is a small **Spring Boot** application designed for straightforward local execution and deployment. It includes a `Dockerfile`, `docker-compose.yml`, Maven configuration, and deployment guidance, which makes it useful as a public sample repository for Java container workflows.[3]

Because the application is intentionally simple, it works well as a reference example for developers who want to validate Docker-based deployment, test a minimal Java service, or try a sample deployment flow on [Nife.io](https://nife.io).[1]

## Features

| Feature | Description |
| --- | --- |
| Spring Boot application | Minimal Java application with a simple response endpoint |
| Docker support | Includes a `Dockerfile` for image build and runtime |
| Docker Compose support | Includes `docker-compose.yml` for local execution |
| Maven build | Uses `pom.xml` for dependencies and build configuration |
| Kubernetes example | Includes an optional Minikube-based deployment flow |
| Nife.io deployment sample | Suitable as a sample project for [Nife.io](https://nife.io) |

## Tech Stack

| Technology | Purpose |
| --- | --- |
| Java | Application runtime |
| Spring Boot | Web framework |
| Maven | Build and dependency management |
| Docker | Container packaging and execution |
| Docker Compose | Local container orchestration |
| Nife.io | Deployment platform |

## Prerequisites

Before running this project, make sure the following tools are available.

| Requirement | Notes |
| --- | --- |
| Docker | Required for container build and runtime |
| Git | Required to clone the repository |
| Java | Optional for non-container local development |
| Maven | Optional if building outside Docker |
| Docker Compose | Optional for Compose-based local execution |

## Getting Started

### Clone the repository

```bash
git clone https://github.com/nifetency/docker-hello-world-spring-boot.git
cd docker-hello-world-spring-boot
```

### Build the Docker image

```bash
docker build -t hello-world-java .
```

The Maven build is executed during the Docker image build process.

### Run the container

```bash
docker run -p 8080:8080 -it --rm hello-world-java
```

### Test the application

```bash
curl http://localhost:8080
```

Expected response:

```text
Hello World
```

## Run with Docker Compose

If you prefer Docker Compose, use the following commands.

```bash
docker-compose up -d
curl http://localhost:8080
docker-compose down
```

## Optional Kubernetes Example

This repository can also be used with a local Kubernetes cluster such as Minikube.[3]

```bash
minikube start
kubectl create deployment hello-spring-boot --image=dstar55/docker-hello-world-spring-boot:latest
kubectl expose deployment hello-spring-boot --type=NodePort --port=8080
minikube service hello-spring-boot --url
```

After the service URL is generated, test it with `curl`.

## Deploy on Nife.io

You can deploy this application on [Nife.io](https://nife.io) either from a Docker image or directly from the Git repository.[1] [2]

### Option 1: Deploy from a Docker image

First, build and push the image to a container registry.

```bash
docker build -t hello-world-java .
docker tag hello-world-java <username>/hello-world-java:latest
docker push <username>/hello-world-java:latest
```

Then create a new application in Nife.io using the following settings.

| Setting | Value |
| --- | --- |
| Source | Docker Image |
| Image | `<username>/hello-world-java:latest` |
| Internal Port | `8080` |
| External Port | `80` |
| Suggested Replicas | `1` |
| Suggested Memory | `512MB` to `1GB` |
| Suggested CPU | `250m` to `500m` |

### Option 2: Deploy from the Git repository

You can also deploy directly from GitHub.

| Setting | Value |
| --- | --- |
| Source | Git Repository |
| Provider | GitHub |
| Repository | `nifetency/docker-hello-world-spring-boot` |
| Branch | `master` |
| Internal Port | `8080` |
| External Port | `80` |
| Build Mode | Auto-Dockerize with runtime |

### Option 3: Deploy with `nifectl`

If you prefer the CLI workflow, use the following commands.

```bash
nifectl auth login
nifectl init
nifectl deploy
```

For the full CLI setup, see the [Nifectl Quick Start documentation](https://docs.nife.io/Quick-Start/Nifectl).[2]

## Repository Structure

| Path | Purpose |
| --- | --- |
| `src/` | Java source code and tests |
| `Dockerfile` | Container build instructions |
| `docker-compose.yml` | Compose-based local workflow |
| `pom.xml` | Maven project configuration |
| `Jenkinsfile` | CI pipeline example |
| `.gitlab-ci.yml` | Additional CI configuration |

## Configuration Notes

| Item | Value |
| --- | --- |
| Application port | `8080` |
| Main build file | `pom.xml` |
| Default branch | `master` |
| License | `MIT` |

## Troubleshooting

| Issue | Suggested fix |
| --- | --- |
| Port `8080` is already in use | Stop the conflicting service or change the host port mapping |
| Docker build fails | Confirm Docker is running and rebuild the image |
| Application does not respond | Check the container logs and confirm the app is bound to `8080` |
| Registry push fails | Verify container registry authentication and image name |
| Nife.io deployment fails | Recheck source selection, port configuration, and deployment logs |

## Acknowledgements

This repository is based on the original [`dstar55/docker-hello-world-spring-boot`](https://github.com/dstar55/docker-hello-world-spring-boot) project and has been adapted by **Nifetency** as a sample deployment repository for [Nife.io](https://nife.io).[3]

## License

This project is licensed under the **MIT License**. See the `LICENSE` file for details.

## References

[1]: https://nife.io "Nife.io"
[2]: https://docs.nife.io/Quick-Start/Nifectl "Nifectl Quick Start"
[3]: https://github.com/nifetency/docker-hello-world-spring-boot "nifetency/docker-hello-world-spring-boot"
