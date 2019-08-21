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
docker stop [container]
```

Clean up stopped containers, build cache, dangling images:
``` docker system prune ```


