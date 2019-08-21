### Useful docker commands
```
docker images  - shows images
docker rmi ... - remove image
docker rm ...  - remove container
docker ps -a   - active container list
git branch -a  - all branches
git branch     - current branch
git status     - status of current branch
git checkout --track ... - switch to a specific branch
docker build --no-cache -t [any build name] .
```


Default docker run command:
```
docker run [image]
docker run busybox
```

Docker run with alternative command to run on start of the containter:
``` 
docker run [image] [command] 
docker run busybox echo hello hello my friend!
docker run busybox ls
docker run busybox ping google.com
docker run -it [image] sh # runs an image with shell 
```

Docker run with port forwarding:
```
docker run -p [localport:containerport] [image]
docker run -p 8080:8080 redis
```

Docker run without attaching to the container:
```
docker -d [image]
```

List running containers or all containers:
```
docker ps
docker ps -a
```

Creating, starting and stopping a container:
```
docker create [image]
docker start [container]
docker start -a [container] # Attaches to the container, watches for output
docker stop [container] # Clean stop
docker kill [container] # Rough stop
```

Clean up stopped containers, build cache, dangling images:
```
docker system prune 
```

One liner to stop / remove all of Docker containers:
```
docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)
```

Check logs of a container:
```
docker logs [container]
```

Executing commands on an already running container: (note: -it allows input from user)
```
docker exec -it [container] [command] 
docker exec -it [redis-container-id] redis-cli
docker exec -it [container] sh # opens a terminal inside a running container!
```

Dockerfile example: (used to build a custom image)
```
# Base image:
FROM node:alpine

# Specifying working directory in the base image:
WORKDIR '/app'

# Copying node dependency file from current folder to working directory and fetching the necessary dependencies:
COPY package.json .
RUN npm install

# Copying the rest of the files from current folder to working directory:
COPY . .

# Assigning a default start command:
CMD ["npm","run","start"]
```

Creating an image from a Dockerfile that is in the current folder:
```
docker build .

docker build -t [image-name-tag] . # assigns the image a custom name
docker build -t username/projectname:version . # tagging convetion

docker build -f [Dockerfile name] # specify a specific file to be used as the Dockerfile for the build
docker build -f Dockerfile.dev
```

docker-compose.yml example:
```
version:'3'
services:
  redis-server:
    image: 'redis'
  node-app:
    restart: always
    build: .
    ports:
      - "4001:8081"
```

Using docker-compose:
```
docker-compose up
docker-compose up --build # used to rebuild
docker-compose down # stop all running containers related to the docker-compose file in current directory, remove them as well
docker-compose ps # check status of containers related to the docker-compose file in current directory
```
