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

