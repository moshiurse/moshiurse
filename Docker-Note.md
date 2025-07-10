# Docker Notes

### Virtual machine vs Container

| Virtual machine | Container |
| ----------- | ----------- |
| An abstraction of a matchine (physical hardware) **Hypervisor** Vmware/Virtualbox | An Isolated environment for running an application |
| Runs a complete operating system including the kernel, thus requiring more system resources (CPU, memory, and storage) | Runs the user mode portion of an operating system, and can be tailored to contain just the needed services for your app, using fewer system resources. |
|Slows to start | Start quickly, lightweight |
|Need more hardware | Need less hardware |
|Use full blown OS | Use Os of the host |

### Docker Architecture

![image](https://github.com/user-attachments/assets/b5649fe7-44ad-425d-8394-0ef6c473dbea)

![image](https://github.com/user-attachments/assets/b21c10a0-c32c-49f7-b27d-c002c6791d5d)




### Install Docker

[Get started with Docker](https://www.docker.com/get-started/)


[Install wsl for windows](https://learn.microsoft.com/en-us/windows/wsl/install)

### Dev workflow

**What is image?**

- A cut-down OS
- A runtime environment
- Contains Application files
- Contains Third party libraries
- Contains Environment variables

### Procedure

```
FROM node:alpine
COPY . /app
WORKDIR /app

CMD node app.js
```

`docker build -t hello-docker .`

To check docker images list

`docker image ls` OR `docker images`

```
REPOSITORY   TAG     IMAGE ID      CREATED            SIZE
hello-docker latest  7b6c118df339  About a minute ago 163MB
```
Run Docker image using `docker run hello-docker`

For pulling any images `docker pull ubuntu`

For pull and run any images `docker run ubuntu`

See the list of running images `docker ps`

See the list of all images `docker ps -a` OR `docker ps --all`

`docker ps -all` command will return just last created container.

To start a container with interactive mode `docker run -it ubuntu`
