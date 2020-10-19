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
docker run -it ubuntu sh -c 'apt-get update; apt-get install curl; echo "Input website:"; read website; echo "Searching.."; sleep 1; curl http://$website;'
```