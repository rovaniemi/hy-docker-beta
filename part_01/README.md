## 1.1

Commands

```
docker run -d postgres
docker run -d nginx
docker run -d node
docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS                     PORTS               NAMES
f290680ee80d        node                "node"                   8 seconds ago        Up About a minute                              optimistic_leavitt
d75bc90c228e        nginx               "nginx -g 'daemon of…"   About a minute ago   Up About a minute          80/tcp              hopeful_banach
06c5127e59ea        postgres            "docker-entrypoint.s…"   About a minute ago   Up About a minute          5432/tcp            elastic_lamport

docker stop f290680ee80d d75bc90c228e
docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS                     PORTS               NAMES
06c5127e59ea        postgres            "docker-entrypoint.s…"   About a minute ago   Up About a minute          5432/tcp            elastic_lamport
```

## 1.2

Commands

```
docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS                     PORTS               NAMES
06c5127e59ea        postgres            "docker-entrypoint.s…"   About a minute ago   Up About a minute          5432/tcp            elastic_lamport

docker stop 06c5127e59ea
docker ps -a

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                      PORTS               NAMES
f290680ee80d        node                "node"                   4 minutes ago       Exited (0) 4 minutes ago                        optimistic_leavitt
d75bc90c228e        nginx               "nginx -g 'daemon of…"   5 minutes ago       Exited (0) 32 seconds ago                       hopeful_banach
06c5127e59ea        postgres            "docker-entrypoint.s…"   5 minutes ago       Exited (0) 32 seconds ago                       elastic_lamport

docker rm f2 d7 06
docker ps -a

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                      PORTS               NAMES

docker images

REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
postgres            latest              f9b577fb1ed6        3 days ago          311MB
node                latest              e6825fa3bd20        4 days ago          895MB
nginx               latest              568c4670fa80        4 days ago          109MB

docker rmi f9 e6 56
docker images

REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
```

## 1.3

Dockerfile

```
FROM ubuntu:16.04

WORKDIR /home
RUN apt-get update && apt-get install -y curl
```

Commands

```
docker build -t curl .
docker run -d --rm -it --name curler curl sh -c 'read website; sleep 3; curl http://$website'
docker attach curl
google.com

<HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
<TITLE>301 Moved</TITLE></HEAD><BODY>
<H1>301 Moved</H1>
The document has moved
<A HREF="http://www.google.com/">here</A>.
</BODY></HTML>
```

## 1.4

Dockerfile

```
FROM ubuntu:16.04
EXPOSE 5000

RUN apt-get update && apt-get install -y git curl
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt install -y nodejs
RUN git clone https://github.com/docker-hy/frontend-example-docker

WORKDIR /frontend-example-docker
RUN npm install
CMD npm start
```

Commands

```
docker build -t node-frontend .
docker run -d -p 5000:5000 node-frontend
```

## 1.5

Dockerfile

```
FROM ubuntu:16.04
EXPOSE 8000

RUN apt-get update && apt-get install -y git curl
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt install -y nodejs
RUN git clone https://github.com/docker-hy/backend-example-docker

WORKDIR /backend-example-docker
RUN touch logs.txt
RUN npm install

CMD npm start
```

Commands

```
docker build -t node-backend .
docker run -d -v $(pwd)/logs.txt:/backend-example-docker/logs.txt -p 8000:8000 node-backend
```

# 1.6

Frotend dockerfile

```
FROM ubuntu:16.04
EXPOSE 5000

RUN apt-get update && apt-get install -y git curl
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt install -y nodejs
RUN git clone https://github.com/docker-hy/frontend-example-docker

WORKDIR /frontend-example-docker
RUN npm install
CMD API_URL=http://localhost:8000 npm start
```

Backend dockerfile

```
FROM ubuntu:16.04
EXPOSE 8000

RUN apt-get update && apt-get install -y git curl
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt install -y nodejs
RUN git clone https://github.com/docker-hy/backend-example-docker

WORKDIR /backend-example-docker
RUN touch logs.txt
RUN npm install

CMD FRONT_URL=http://localhost:5000 npm start
```

Commands

```
docker build -t node-frontend .
docker run -d -p 5000:5000 node-frontend
docker build -t node-backend .
docker run -d -v $(pwd)/logs.txt:/backend-example-docker/logs.txt -p 8000:8000 node-backend
```

## 1.7

Run [this](https://github.com/rovaniemi/exam-archive-prototype) prototype application in port 3000

```
docker run -d -p 3000:3000 tarpisto-proto
```
