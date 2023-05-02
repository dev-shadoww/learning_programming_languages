# Learning Docker

## Introduction

```bash
docker run redis
```

Here `docker cli`, reached out to `docker hub` and downloaded a file called `image`, this single file `image` contains all the dependencies and configurations to run the program, this `image` can be used to create a `container` it is an instance if the `image`.

`image` is made up of `FS Snapshot` and `startup command`,

```bash
docker run hello-world
```

To generate this message, Docker took the following steps:

- The Docker client contacted the Docker daemon.
- The Docker daemon pulled the "hello-world" image from the Docker Hub.
  (amd64)
- The Docker daemon created a new container from that image which runs the
  executable that produces the output you are currently reading.
- The Docker daemon streamed that output to the Docker client, which sent it
  to your terminal.

## Manipulating containers with docker client

### docker commands

- `docker run image-name`, create a container and run it, `docker run image-name command-name`, this form can be used to overwrite default command, but the command should be present in `File System Snapshot`.

- `docker ps`, List all running containers, `--all` options list all the containers that have been executed.

- `docker create image-name`, it creates a container and returns it's `id`, then `docker start -a container-id` starts the container.

- `docker system prune`, delete all the containers.

- `docker logs container-id`, get logs from the containers.

- `docker stop container-id`, or `docker kill container-id`, are used to stop the containers, `stop` issues `SIGTERM` signal and `kill` issues `SIGKILL` signal.

- `docker exec -it container-id command`, execute additional command.

### Building docker images

To build a image first create a `dockerfile` which contains all the configurations, then it is passed to `docker-client`, and then to `docker-server` which creates a usable `docker-image`.

Here `FROM`, `RUN` and `CMD` are instructions to docker server, to build image run `docker build .` command.

```dockerfile
FROM alpine
RUN apk add --update redis
CMD ["redis-server"]
```

adding a tag name to image,

`dockerID / repoName : version`, it can be used as,

```bash
docker build -t linuxMachine/redis:latest .
```

during building use `COPY` command to copy the build files to the container,

```dockerfile
FROM node:alpine

WORKDIR /usr/app

COPY ./ ./
RUN npm install

CMD ["npm", "start"]
```

`building image`,

```bash
docker build -t linuxMachine/simpleWeb .
```

`docker run` with `port mapping`,

```bash
docker run -p 8080:8080 linuxMachine/simpleWeb
```