# Docker Day 1

# Introduction
Name

Professional Experience

Fun Fact :)

## Prerequisite
* Docker desktop
```
$ docker version
Client:
 Cloud integration: 1.0.14
 Version:           20.10.6
 API version:       1.41
 Go version:        go1.16.3
 Git commit:        370c289
 Built:             Fri Apr  9 22:46:57 2021
 OS/Arch:           darwin/amd64
 Context:           default
 Experimental:      true

Server: Docker Engine - Community
 Engine:
  Version:          20.10.6
  API version:      1.41 (minimum version 1.12)
  Go version:       go1.13.15
  Git commit:       8728dd2
  Built:            Fri Apr  9 22:44:56 2021
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.4.4
  GitCommit:        05f951a3781f4f2c1911b05e61c160e9c30eaa8e
 runc:
  Version:          1.0.0-rc93
  GitCommit:        12644e614e25b05da6fd08a38ffa0cfe1903fdec
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0
```
* Visual studio code 
```
$ code -v
1.59.1
3866c3553be8b268c8a7f8c0482c0c0177aa8bfa
x64
```
* Git
```
$ git version
git version 2.15.0
```
* Docker hub account
```
$ docker login
Authenticating with existing credentials...
Login Succeeded
```
* Github account

## What is Docker
Docker is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly.
## What is Container
Container is a place to run an image
## What is Image
Image is a set of code, runtime, and library

## Docker Architecture
![](https://docs.docker.com/engine/images/architecture.svg)

# Docker build
Ref: https://docs.docker.com/engine/reference/builder/

Basic build
1. Check file structure
2. Install flask
```
docker build -t footprns/flask:0.1 ./dockerfile1
docker run --rm footprns/flask:0.1
```

Build app
```
docker build -t footprns/flask:0.2 ./dockerfile2 && \
docker run --rm -p 5000:5000 footprns/flask:0.2
```

Use Environment variable
```
docker build -t footprns/flask:0.2 \
./dockerfile2 && \
docker run --rm \
--env  FLASK_APP=hello.py -p 5000:5000 footprns/flask:0.2
```
Test
```
curl http://localhost:5000
```
fix 
```
docker run --rm -p 5000:5000 --name flask-container footprns/flask:0.2
```
Docker command
```
docker ps |grep flask-container
docker logs flask-container
docker container inspect flask-container
```

# Docker pull
Example: `docker pull nginx`
# Docker run
Example: `docker run -it --rm busybox`

# Docker Volume
```
docker volume create glintz_storage
docker run --rm -it --name glintz \
-v glintz_storage:/var/glintz_data \
--env FLASK_APP=hello.py \
footprns/glintz:0.1
```
check the storage
```
docker exec glintz touch /var/glintz_data/1.txt
docker exec glintz touch /usr/src/1.txt

docker exec glintz ls /var/glintz_data/1.txt
docker exec glintz ls /usr/src/1.txt
docker volume inspect glintz_storage
```

# Docker Network
Bridge
```
docker run --rm -d -v mysql:/var/lib/mysql \
  -v mysql_config:/etc/mysql -p 3306:3306 \
  --network mysqlnet \
  --name mysqldb \
  -e MYSQL_ROOT_PASSWORD=p@ssw0rd1 \
  mysql
```
Host

Overlay