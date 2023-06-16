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
- The Docker daemon created a new container from that image which runs the
  executable that produces the output you are currently reading.
- The Docker daemon streamed that output to the Docker client, which sent it
  to your terminal.

## Manipulating containers with docker client

### docker commands

- `docker run <image-name>`, create a container and run it, `docker run <image-name> <command-name>`, this form can be used to overwrite default command, but the command should be present in `File System Snapshot`.

- `docker ps`, List all running containers, `--all` options list all the containers that have been executed.

- `docker create <image-name>`, it creates a container and returns it's `id`.

- `docker start -a <container-id>` starts the container, `-a` makes the docker to watch the output.

- `docker system prune`, delete all the containers.

- `docker logs <container-id>`, get logs from the containers.

- `docker stop <container-id>`, or `docker kill <container-id>`, are used to stop the containers, `stop` issues `SIGTERM` signal and `kill` issues `SIGKILL` signal.

- `docker exec -it <container-id> <command-name>`, execute additional command.

- `docker exec -it <container-id> sh`, execute terminal commands, `docker run -it busybox sh`.

### Building docker images

To build a image first create a `Dockerfile` which contains all the configurations, then it is passed to `docker-client`, and then to `docker-server` which creates a usable `docker-image`.

Here `FROM`, `RUN` and `CMD` are instructions to docker server, to build image run `docker build .` command.

```dockerfile
FROM alpine
RUN apk add --update redis
CMD ["redis-server"]
```

adding a tag to image,

`dockerID / repoName : version`, it can be used as,

```bash
docker build -t linux/redis:latest .
```

`docker commit -c 'CMD ["<command-name>"]'` to create images manually,

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
docker build -t linux/simpleWeb .
```

`docker run` with `port mapping`,

```bash
docker run -p 8080:8080 linux/simpleWeb
```

## Docker compose with multiple local containers

### Docker Compose

There are two options for connecting different docker containers,

- Using Docker CLI
- Using Docker Compose

`Docker Compose` is used to start multiple docker containers at the same time.

To start using the `Docker Compose` create a `docker-compose.yml` file with all the `docker-cli` commands.

`docker-compose.yml`

```yml
version: "3"
services:
  redis-server:
    image: "redis"
  node-app:
    restart: always
    build: .
    ports:
      - "4001:8081"
```

The service names such as `redis-server` can be directly used in the code, and docker will automatically set up all networking setup and allows the connection to the specified container.

`docker-compose` commands, use `-d` option to run in background,

- `docker-compose up`
- `docker-compose up --build`
- `docker-compose down`
- `docker-compose ps`

`Restart Policies`,

- `"no"`, Never attempt to restart,
- `always`, Always try to restart it,
- `on-failure`, Only start if the container stops with error code,
- `unless-stopped`, Always restart unless we forcibly stop it,

### Setting up docker for node server

```dockerfile
FROM node:alpine

WORKDIR '/app'
COPY package.json .
RUN npm install
COPY . .

CMD ["npm","start"]
```

## Production grade workflow

The flow is development, testing and deployment, in a project there are two `Dockerfiles` one for development version and one for production version.

To build from a different docker file use `-f` option, `docker build -f Dockerfile.dev .`

### Docker volumes

`Docker Volumes` are references to the files in the working directory, The volumes needs to be bookmarked.

```bash
docker run -p 3000:3000 -v /app/node_modules -v $(pwd):/app 68dab4h22c
```

Here `$(pwd):/app` means to map the `pwd` into `/app` directory.

Use the node_modules from `/app`, but for other files reference to the files from current working directory.

```yml
version: "3"
service:
  web:
    build:
      context: .
      dockerfile: Dockerfile.dev
    ports:
      - "3000:3000"
    volumes:
      - /app/node_modules
      - .:/app
```

### Multi setup docker builds

We need multiple docker builds because the alpine image doesn't know about the nginx, and we only need build contents and not the node_modules so in the first part we will build the project and then we will copy everything from first phase to the second phase and start nginx server.

```dockerfile
FROM node:alpine as builder
WORKDIR '/app'
COPY package.json .
RUN npm install
COPY . .
RUN npm run build

FROM nginx
EXPOSE 80
COPY --from=builder /app/build /usr/share/nginx/html
```

### Travis CI

Configuring Travis CI, Create `.travis.yml` file, here Travis CI assumes that the `script` commands completes it's execution.

Here we are using Travis CI with AWS Elastic BeanStalk, it creates a load balancer which automatically routes the traffic if the connections reaches the threshold.

```yaml
sudo: required
services:
  - docker

before_install:
  - docker build -t linux/example -f Dockerfile.dev .

script:
  - docker run linux/example npm run test -- --coverage

deploy:
  provider: elasticbeanstalk
  region: "us-west-2"
  app: "docker"
  env: "docker-env"
  bucket_name: "bucket-name"
  bucket_path: "docker"
  on:
    branch: master
  access_key_id: $AWS_ACCESS_KEY
  secret_access_key:
    secret: "$AWS_SECRET_KEY"
```

## Building multi container applications

Here the project uses React, Express and a Worker node, now creating `dev docker files`.

`Dockerfile.dev` for Client,

```dockerfile
FROM node:alpine
WORKDIR '/app'
COPY ./package.json ./
RUN npm install
COPY . .
CMD ["npm", "run",  "start"]
```

`Dockerfile.dev` for Server,

```dockerfile
FROM node:alpine
WORKDIR '/app'
COPY ./package.json ./
RUN npm install
COPY . .
CMD ["npm", "run", "dev"]
```

`Dockerfile.dev` for Worker,

```dockerfile
FROM node:alpine
WORKDIR '/app'
COPY ./package.json ./
RUN npm install
COPY . .
CMD ["npm", "run", "dev"]
```

Adding docker compose files to the project,

`docker-compose.yml`,

```yaml
version: 3
services:
  postgres:
    image: "postgres:latest"
  redis:
    image: "redis:latest"
  server:
    build:
      dockerfile: Dockerfile.dev
      context: ./server/
    volumes:
      - /app/node_modules
      - ./server:/app
```
