---
title: "Manipulate a docker image and launch a notebook"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
# Basics

### In a nutshell:
``` bash
docker build -t imagename:local -f Dockerfile ./
docker run --rm -it imagename:local /bin/bash
docker push dockerhubname
VERSION=`git tag -l |sort -V | tail -1 | sed 's/v//'`
docker tag dockerhubname dockerhubname:$(VERSION)
docker push dockerhubname:$(VERSION)
```

### Checkout docker image from repo to test it
``` bash 
$ docker build -t imagename:local ./
$ docker run --rm -it imagename:local  /bin/bash
```
 > `root@6efdfbae85a8:/#`
Then in another terminal: `docker cp $HOME/path/to/project 6efdfbae85a8:/root/project` to get the project inside for testing.


### Docker build
``` bash 
docker build -t hello-world:1.0 .
```

### Run image
``` bash 
docker run -p 8080:80 --name hello -d hello-world:1.0
```

### Tag image
``` bash 
docker tag hello-world user/hello-world
```

### Push image to docker hub
``` bash 
docker push <Your Docker ID>/hello-world
```

### Pull image to docker hub
``` bash 
docker pull user/hello-world
```

### See existing images
``` bash 
docker images
```

### See what is running 
``` bash 
docker ps
docker ps -a # show images, even ones stopped
```

### Start docker process
``` bash 
docker start <container NAME> # from `docker ps -a`
```

### Stop and remove image
``` bash 
# Stop docker container from running
docker stop <container NAME>
# removes from both `docker ps` and `docker ps -a`
docker rm <container NAME>

# Replace above with
docker rm -f <container NAME>
```

### Docker logs
``` bash 
docker logs -f <container NAME> # -f to follow and listen
```


# Advanced

### Clean your environment

``` bash 
# running processes
docker ps -a
docker stop <CONTAINER ID>
docker rm <CONTAINER ID>

# Clean open images
docker images
docker rmi <IMAGE ID or REPOSITORY>

# Prune system to close all communication
docker system prune -f
```

### Show the history of a docker image 
``` bash 
docker images # get <IMAGE ID>
docker history --no-trunc <IMAGE ID> # without runcation
```

### Build docker image 
``` bash 
docker build -f Dockerfile -t othrif:mytest .
docker run -p 5000:5000 othrif:mytest 
# Let your local host recognize the server
sudo emacs /private/etc/hosts
# add the notebok address from running the line "The Jupyter Notebook is running at:http://XXXXXX:5000/"
# by adding `XXXXXX` to `127.0.0.1	localhost XXXXXX`
```

### Run interactively
``` bash 
docker ps -a # get <IMAGE> and <CONTAINER ID>
docker run -d -it -p 8000:8080 <IMAGE> /usr/bin/top # <IMAGE>=othrif:mytest
docker exec -it <CONTAINER ID> /bin/bash

```

Alternatively run interactively and remove image after exit
``` bash 
docker run --rm -it <IMAGE> /bin/bash
```

### Start Docker deamon
``` bash 
docker-machine start
docker-machine env
eval $(docker-machine env)
```

# Docker compose

### Build and run app
```
docker-compose up -d
```

### Stop app
``` 
docker-compose down
```


### docker-compose.yml
Examples 
``` python
version: "3.8"
services:
  web:
    build: .
    ports:
      - "5000:5000"
  redis:
    image: "redis:alpine"
```


```python

```
