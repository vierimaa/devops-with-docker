# DevOps with Docker
## Part 1 exercises

### Exercise 1.1

```
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                          PORTS               NAMES
f88da6ee5ad2        nginx               "/docker-entrypoint.…"   2 minutes ago       Exited (0) About a minute ago                       quizzical_fermat
23e9159167da        nginx               "/docker-entrypoint.…"   2 minutes ago       Exited (0) About a minute ago                       elastic_banach
f3b383924c79        nginx               "/docker-entrypoint.…"   2 minutes ago       Up 2 minutes                    80/tcp              youthful_swartz
10e9935cebdc        nginx               "/docker-entrypoint.…"   About an hour ago   Exited (0) About an hour ago                        naughty_brown
2cc8441cc194        nginx               "/docker-entrypoint.…"   About an hour ago   Exited (0) About an hour ago                        amazing_lichterman
```

### Exercise 1.2

```
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES               SIZE
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
```

### Exercise 1.3

```
$ docker pull devopsdockeruh/pull_exercise
$ docker run -it devopsdockeruh/pull_exercise
Give me the password: basics
You found the correct password. Secret message is:
"This is the secret message
```

### Exercise 1.4

```
Secret message is:
"Docker is easy"
Mon, 19 Oct 2020 18:04:10 GMT
Mon, 19 Oct 2020 18:04:13 GMT
Mon, 19 Oct 2020 18:04:16 GMT
Mon, 19 Oct 2020 18:04:19 GMT
Secret message is:
"Docker is easy"
```

### Exercise 1.5

```
$ docker run -it ubuntu sh -c 'apt-get update; apt-get install curl; echo "Input website:"; read website; echo "Searching.."; sleep 1; curl http://$website;'
```

### Exercise 1.6

Dockerfile
```
FROM devopsdockeruh/overwrite_cmd_exercise
CMD ["-c"]
```

Commands
```
$ docker build -t docker-clock .
$ docker run docker-clock
```

### Exercise 1.7

Dockerfile
```
FROM ubuntu:16.04 
WORKDIR /mydir
RUN apt-get update && apt-get install -y curl 
COPY myscript.sh .
CMD ./myscript.sh
```

Script file
```
#!/bin/sh
echo "Input website:"; read website; echo "Searching.."; sleep 1; curl http://$website;
```

Commands
```
$ docker build -t curler .
$ docker run --rm -it curler
```

Output
```
Input website:
helsinki.fi
Searching..
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>301 Moved Permanently</title>
</head><body>
<h1>Moved Permanently</h1>
<p>The document has moved <a href="http://www.helsinki.fi/">here</a>.</p>
</body></html>
```

### Exercise 1.8

Commands
```
$ docker run -v $(pwd)/logs.txt:/usr/app/logs.txt devopsdockeruh/first_volume_exercise
```

Output
```
Tue, 20 Oct 2020 17:17:14 GMT
Tue, 20 Oct 2020 17:17:17 GMT
Tue, 20 Oct 2020 17:17:20 GMT
Tue, 20 Oct 2020 17:17:23 GMT
Secret message is:
"Volume bind mount is easy"
```

### Exercise 1.9

Commands
```
$ docker run -d -p 8000:80 devopsdockeruh/ports_exercise
```

### Exercise 1.10

Dockerfile
```
FROM node:alpine
WORKDIR /usr/src/app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 5000
CMD [ "npm", "start" ]
```

### Exercise 1.11

Dockerfile
```
FROM node:alpine
WORKDIR /usr/src/app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 8000
CMD [ "npm", "start" ]
```

Commands
```
$ docker build -t backend-example .
$ docker run -v $(pwd)/logs.txt:/usr/src/app/logs.txt -p 8000:8000 backend-example
```

logs.txt
```
10/20/2020, 7:40:02 PM: Connection received in root
10/20/2020, 7:40:09 PM: Connection received in root
```

### Exercise 1.12

Dockerfile frontend
```
FROM node:alpine
WORKDIR /usr/src/app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 5000
CMD [ "npm", "start" ]
```

Dockerfile backend
```
FROM node:alpine
WORKDIR /usr/src/app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 8000
CMD [ "npm", "start" ]
```

Commands
```
$ docker build -t frontend .
$ docker build -t backend-example .
$ docker run -p 5000:5000 -d frontend
$ docker run -v $(pwd)/logs.txt:/usr/src/app/logs.txt -p 8000:8000 backend
```

### Exercise 1.13

Dockerfile frontend
```
FROM openjdk:8-alpine
EXPOSE 8080
WORKDIR /app
COPY . .
RUN ./mvnw package
CMD ["java", "-jar", "./target/docker-example-1.1.3.jar"]
```

Commands
```
$ docker build -t spring-example-project .    
$ docker run -p 8080:8080 spring-example-project
```

### Exercise 1.14

Dockerfile frontend
```
FROM ruby:2.6.0
EXPOSE 3000
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt install -y nodejs
COPY . .
RUN bundle install
RUN rails db:migrate
CMD ["rails","s"]
```

Commands
```
$ docker build -t rails-example-project .   
$ docker run -p 3000:3000 rails-example-project
```

### Exercise 1.15

Dockerhub link

> https://hub.docker.com/repository/docker/vierimaa/blogapp

### Exercise 1.16

Heroku link

> https://devopsdocker16.herokuapp.com/

### Exercise 1.17

Dockerfile
```
FROM python:3.8
WORKDIR /code
RUN pip install --no-cache-dir numpy pandas tensorflow matplotlib SciPy
```