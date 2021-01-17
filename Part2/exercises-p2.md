# DevOps with Docker
## Part 2 exercises

### Exercise 2.1

docker-compose.yml
```
version: '3.5'

services:
    first_volume_excercise:
        image: devopsdockeruh/first_volume_exercise
        volumes:
            - ./logs.txt:/usr/app/logs.txt
```

Commands
```
$ docker-compose up -d
```

### Exercise 2.2

docker-compose.yml
```
version: '3.5'

services:
    ports_exercise:
        image: devopsdockeruh/ports_exercise
        ports:
          - 80:80
```

Commands
```
$ docker-compose up -d
```

### Exercise 2.3

docker-compose.yml
```
version: '3.5'

services:
    frontend:
        image: frontend
        ports:
            - 5000:5000
    backend:
        image: backend-example
        ports:
          - 8000:8000
        volumes:
            - ./logs.txt:/usr/src/app/logs.txt
```

Commands
```
$ docker-compose up -d
```

### Exercise 2.4

Commands
```
docker-compose up -d --scale compute=3
```

### Exercise 2.5

docker-compose.yml
```
version: '3.5'

services:
    frontend:
        image: frontend
        ports:
          - 5000:5000
    backend:
        image: backend-example
        ports:
          - 8000:8000
        volumes:
          - ./logs.txt:/usr/src/app/logs.txt
        environment:
          - REDIS=redis
          - REDIS_PORT=6379
        restart: unless-stopped
    redis:
        image: redis
```

Commands
```
$ docker-compose up -d
```

### Exercise 2.6

docker-compose.yml
```
version: '3.5'

services:
  frontend:
    image: frontend
    ports:
      - 5000:5000
  backend:
    image: backend
    ports:
      - 8000:8000
    volumes:
      - ./logs.txt:/usr/src/app/logs.txt
    environment:
      - REDIS=redis
      - REDIS_PORT=6379
      - DB_USERNAME=admin
      - DB_PASSWORD=s3cr37
      - DB_HOST=db
    restart: unless-stopped
    depends_on:
      - db
  redis:
    image: redis
  db:
    image: postgres
    restart: unless-stopped
    environment:
      - POSTGRES_USER=admin
      - POSTGRES_PASSWORD=s3cr37
```

Commands
```
$ docker-compose up -d
```


### Exercise 2.8

docker-compose.yml
```
version: '3.5'

services:
  ngnix:
    image: nginx
    ports:
      - 80:80
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf
    depends_on:
        - frontend
        - backend

  frontend:
    image: frontend
    ports:
      - 5000:5000
    environment:
      - API_URL=http://localhost/api

  backend:
    image: backend
    ports:
      - 8000:8000
    volumes:
      - ./logs.txt:/usr/src/app/logs.txt
    environment:
      - REDIS=redis
      - REDIS_PORT=6379
      - DB_USERNAME=admin
      - DB_PASSWORD=s3cr37
      - DB_HOST=db
    restart: unless-stopped
    depends_on:
      - db

  redis:
    image: redis

  db:
    image: postgres
    restart: unless-stopped
    environment:
      - POSTGRES_USER=admin
      - POSTGRES_PASSWORD=s3cr37

nginx.conf
```
events { worker_connections 1024; }

http {
  server {
    listen 80;

    location / {
      proxy_pass http://frontend:5000/;
    }

    location /api/ {
      proxy_pass http://backend:8000/;
    }
  }
}
```

Commands
```
$ docker-compose up -d
```