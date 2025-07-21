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

### What is image?
- A cut-down OS
- A runtime environment
- Contains Application files
- Contains Third party libraries
- Contains Environment variables

### What is container?
- Provide an isolated environment
- Can be stopped and restarted
- Just a process

### Dev workflow

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

To exec bash `docker exec -it CONTAINER_ID bash` 

To run docker with sh `docker run -it CONTAINER_ID sh` 

To login as specific user `docker exec -it -u moshiur CONTAINER_ID bash`

### Instructions
**FROM** => Specify the base image<br>
**WORKDIR** => Specify the working directory<br>
**USER** => Specify the user who should run commands or activity<br>
**COPY** => Copy file or directory<br>
**ADD** => Add file or directory<br>
**RUN** => Executing OS command<br>
**ENV** => Setting up environment variable<br>
**EXPOSE** => Expose container to specific port<br>
**CMD** => Expose container to specific port<br>
**ENTRYPOINT** => Specify the command which will be run when started the container<br>

### Sample Docker file for react app

```
FROM 14.16.0-alpine-3.13 //Chose base image node alpine
RUN addgroup app && adduser -S -G app app //create user and usergroup
USER app //set user
WORKDIR /app //If we set it then no need to use /app when copy
COPY package*.json /app/ //It will copy all package*.json file app folder
COPY . . //It will copy all file to app folder
COPY ["hello.txt", "."] we can also use this
ADD . . //we can use direct link to this or also add zip which will extract zip file there

RUN npm install

ENV API_URL=api.com //set env

#exec form
CMD ["npm", "start"]

#shell form
CMD npm start

ENTRYPOINT  ["npm", "start"]


```

Build docker `docker built -t react-app .`

`.dockerignore` will ignore some files or folder Ie: node_modules

`printenv`, `printenv API_URL` OR `$API_URL` to check env variables

We can run docker using `docker run react-app npm start`

But it is not practical, So here comes `Entrypoint & CMD`

`CMD` can be overridden by `docker run react-app npm start` but `Entrypoint` is not overriden by this.

**To optimize** docker build 

```
COPY package*.json .
RUN npm install
COPY . .
```

To remove images `docker image prune`

To remobe containers `docker comtainer prune`

To remove specific image `docker rm IMAGE_ID_OR_NAME`

### Tagging images

On build `docker build react-app:1.0.0 .`

Manually tag `docker image tag react-app:latest react-app:1.0.0`

### Pushing images to hub
`docker image tag react-app:latest moshiurse/react-app:1.0.0`

`docker push moshiurse/react-app:1.0.0`

**Docker image save** `docker image save -o react-app.tar react-app:1.0.0`

**Docker image load** `docker image load -i react-app.tar`

### Containers

Run container in a detached mode `docker run -d react-app`

`docker ps` get all the containers

Run container with name `docker run -d --name blue-bird react-app`

View logs `docker logs CONTAINER_ID` `docker logs -f CONTAINER_ID`

`docker logs -n 10 ID` to log last 10 line
`docker logs -n -t 10 ID` to see timestamp

**Port Publish**  `docker run -d -p 3000:3000 --name=react react-app`

**Execute commands in running container** `docker exec react ls`

Difference of `run` and `exec` is run always create new container but exec is operating on running container.

**Start Container** `docker start react`
**Stop Container** `docker stop react`
**Remove Container** `docker rm react` if your container is runnung then you need to stop first then remove.

You can force remove `docker rm -f react` 

### Filesystem

Each container has its own filesystem.

Volum create `docker volume app-data`<br>
Volume inspect `docker volume inspect app-data`

```
{
    "CreatedAt": "2025-03-04T04:41:09Z",
    "Driver": "local",
    "Labels": {
        "com.docker.volume.anonymous": ""
    },
    "Mountpoint": "/var/lib/docker/volumes/71a9/_data",
    "Name": "app-data",
    "Options": null,
    "Scope": "local"
}
```
Docker run with creating volume `docker run -d -p 4000:3000 -v app-data:/app/data react-app`

to prevent permission issue on creating volume create folder using `USER` `RUN mkdir data`

volumes data remain same even if we delete the container.

Copy file from container to host `docker cp ID:/app/file.txt .`<br>
Copy file from host to container `docker cp secret.txt ID:/app`

So by this we can also share so source code with container so that we get the reflected changes when we changes anything.

`docker run -d -p 5000:3000 -v $(pwd):/app react-app`

But running all these are pain , right ? So here come `Docker compose`

### Docker Compose

The default filename of compose file is `docker-compose.yml`

**Sample File**

```
version: "3.8"
services:
    frontend:
        build: ./frontend
        ports:
            - 3000:3000
    backend:
        build: ./backend
        ports:
            - 3001:3001
        environments:
            DB_URL: mongodb://db/test_db
        volumes:
            - ./backend:/app
        command: ./wait-for db:27017 && migrate-mongo up && npm start
    db:
        image: mongo:4.0-xenial
        ports:
            - 27017:27017
        volumes: 
            - test_db:/data/db
volumes:
    test_db
```

Build using compose `docker compose build`<br>
Build using compose with no cache `docker compose build --no-cache`<br>
Docker up with build `docker compose up --build`<br>
Docker up with detached mode `docker compose up -d`<br>
Check started container `docker compose ps`<br>
Down `docker compose down`

### Docker Network

`docker network ls`

### View Logs

`docker compose logs`

For specific container logs `docker logs ID -f`
