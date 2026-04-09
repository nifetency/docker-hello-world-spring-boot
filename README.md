Hello World sample shows how to deploy [SpringBoot](http://projects.spring.io/spring-boot/) RESTful web service application with [Docker](https://www.docker.com/) and with [Kubernetes](https://kubernetes.io/)

#### Prerequisite 

Installed:   
[Docker](https://www.docker.com/)   
[git](https://www.digitalocean.com/community/tutorials/how-to-contribute-to-open-source-getting-started-with-git)   

Optional:   
[Docker-Compose](https://docs.docker.com/compose/install/)   
[Java 1.8 or 11.1](https://www.oracle.com/technetwork/java/javase/overview/index.html)   
[Maven 3.x](https://maven.apache.org/install.html)


#### Steps

##### Clone source code from git
```
git clone https://github.com/dstar55/docker-hello-world-spring-boot .
```

##### Build Docker image
```
docker build -t="hello-world-java" .
```
Maven build will be executes during creation of the docker image.

>Note:if you run this command for first time it will take some time in order to download base image from [DockerHub](https://hub.docker.com/)

##### Run Docker Container
```
docker run -p 8080:8080 -it --rm hello-world-java
```

##### Test application

```
curl localhost:8080
```

response should be:
```
Hello World
```

#####  Stop Docker Container:
```
docker stop `docker container ls | grep "hello-world-java:*" | awk '{ print $1 }'`
```

### Run with docker-compose 

Build and start the container by running 

```
docker-compose up -d 
```

#### Test application with ***curl*** command

```
curl localhost:8080
```

response should be:
```
Hello World
```

##### Stop Docker Container:
```
docker-compose down
```

### Deploy under the Kuberenetes cluster

#### Prerequisite

##### MiniKube

Installed:
[MiniKube](https://www.digitalocean.com/community/tutorials/how-to-use-minikube-for-local-kubernetes-development-and-testing)

Start minikube with command:
```
minikube start
```


#### Retrieve and deploy application

```
kubectl create deployment hello-spring-boot --image=dstar55/docker-hello-world-spring-boot:latest
```

#### Expose deployment as a Kubernetes Service
```
kubectl expose deployment hello-spring-boot --type=NodePort --port=8080
```

#### Check whether the service is running
```
kubectl get service hello-spring-boot
```

response should something like:
```
NAME                TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
hello-spring-boot   NodePort   xx.xx.xxx.xxx   <none>        8080:xxxxx/TCP   59m
```

#### Retrieve URL for application(hello-spring-boot)
```
minikube service hello-spring-boot --url
```

response will be http..., e.g:
```
http://127.0.0.1:44963
```

#### Test application with ***curl*** command(note: port is randomly created)

```
curl 127.0.0.1:44963
```

response should be:
```
Hello World
```
## Deployment on NIFE

Use this link to acces nife dashboard https://launch.nife.io/

Deploy your Spring Boot application using the NIFE UI:

**Source → Build → Resources → Review → Deploy**

---

### Method 1: Docker Image (Recommended)

#### Step 1: Build & Push Image

```bash
docker build -t hello-world-java .
docker tag hello-world-java <username>/hello-world-java:latest
docker push <username>/hello-world-java:latest
```

---

#### Step 2: Configure in NIFE

* Source → Docker Image
* Image → `<username>/hello-world-java:latest`

**Ports**

* Internal → `8080`
* External → `80`

---

#### Step 3: Resources

* Select Region (e.g., `ap-south-1`)

**Recommended**

* CPU → 250m–500m
* Memory → 512MB–1GB
* Replicas → 1–2

---

#### Step 4: Deploy

Click **Deploy**

---

### Method 2: Git Repository

#### Step 1: Source

* Select GitHub repository
* Branch → `main`

---

#### Step 2: Build

* Internal Port → `8080`
* External Port → `80`
* Enable **Auto-Dockerize with Runtime**

---

#### Step 3: Security

* SAST
* SCA
* Container Scan
* IaC Scan

---

#### Step 4: Resources & Deploy

* Configure resources
* Click **Deploy**

---

## Install nifectl CLI (Windows)

### 1. Download

 https://github.com/nifetency/nifectl/releases

Download:

```text
nifectl-windows-amd64.zip
```

---

### 2. Extract

* Right-click → Extract All
* Open folder

---

### 3. Open Terminal

* Type `cmd` in address bar

OR

* Right-click → Open in Terminal

---

### 4. Verify Installation

```bash
nifectl --help
```

---

## Deployment using nifectl (CLI)

### Prerequisites

* `nifectl` installed
* Access to your NIFE organization

---

### Step 1: Login

```bash
nifectl auth login
```

---

### Step 2: Initialize Project

```bash
nifectl init
```

Follow prompts:

* App Name → auto/manual
* Organization → select
* Source → Repository
* Provider → GitHub
* Branch → `main`

---

### Step 3: Configure Deployment

* Deployment Type → `Deployment`
* Resource Type → `CPU`
* Replicas → `1`

**Ports**

* Internal → `8080`
* External → `80`

---

### Step 4: Deploy Application

```bash
nifectl deploy
```

---

### Step 5: Select Region

* Example:

  * `IND - India, Mumbai`
  * `my-cluster`

---

### Step 6: Monitor Deployment

* Validating configuration
* Building application
* Creating release
* Deploying

---

### Step 7: Access Application

* A public URL will be generated
* Open it in your browser

---

### Notes

* Ensure correct port (`8080`)
* Docker image must be public
* `nife.toml` stores deployment configuration
