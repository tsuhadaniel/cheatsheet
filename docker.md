## Docker

### Images

List
```
docker images
docker image ls
```

Download
```
docker pull [image]
```

Remove
```
docker rmi [image]
```

Information
```
docker history [image]
docker inspect [image]
```

### Containers

List all containers
```
docker container ls -a
docker ps -a
```

Run (create a new container)
```
docker run [options] [image] [command] [args]
```

Start (just if the container already exists)
```
docker start [container]
```

Pause
```
docker pause [container]
docker unpause [container]
```

Stop (kill all processes)
```
docker stop [container]
```

Remove
```
docker rm [container]
docker rm [container] --force
```

Execute a command on a running container
```
docker exec [options] [container] [command] [args]
docker exec [container] ls -l # list files
docker exec [container] sh [file] # run a script
docker exec -it [container] bash # iterative mode
```

Port mapping
```
docker port [container]
docker run -p [local_port]:[container_port] [image]
docker run -P [image]
```

Interactive mode
```
docker run -it [image] [command]
docker run -it

docker run -it python bash
docker run -it -p 8080:5000 campusboard/site
```

Build an image
```
docker build . -t [domain/project:version]
docker build . -t [image id]
docker build . -t campusboard/site
```

Copy files to container
```
docker [files on local machine (origin)] [image id]:[files to the container (destiny)]
docker cp ./pipeline campusboard/pipeline:./
```

#### Storage

Bind mount (local dir)
```
docker run -v [local dir]:[container dir] [image]
docker run --mount type=bind,source=[local dir],target=[container dir] [image]
```

Volume (/var/lib/docker/volumes)
```
docker volume create [volume]
docker volume ls

docker run -v [volume]:[container dir] [image]
docker run --mount source=[volume],target=[container dir] [image]
```

tmpfs (memory)
```
docker run --tmpfs=[temp dir][image]
docker run --mount type=tmpfs,destination=[container dir] [image]
```

### Dockerfile

```
FROM [image base]
RUN [commands]
WORKDIR [path to work dir]
COPY [files on local machine (origin)] [files to the container (destiny)]
# Used during image building
# Can be replaced with --build-arg MY_VAR=new_value
ARG [name=default_value (optional)]
# Used during run time
# Can be replaced with -e MY_VAR=new_value or --env-file=file.env
ENV [name=default_value (optional)]
EXPOSE [port]
ENTRYPOINT [commands (cannot be replaced with -it, only one per file)]
CMD [commands (can be replaced with -it, only one per file)]
```

```
FROM python

RUN curl https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh --output miniconda.sh /
    && bash miniconda.sh -b -p $HOME/miniconda

RUN eval "$($HOME/miniconda/bin/conda shell.bash hook)" \
    && conda init \
    && conda create --name simple-server -y \
    && conda activate simple-server \
    && conda install -y flask \
    && conda install -y pandas

WORKDIR /server
COPY . .

EXPOSE 5000

CMD eval "$($HOME/miniconda/bin/conda shell.bash hook)" \
    && conda activate simple-server \
    && python app.py
```

### Extra

Remove all images and containers 
```
docker system prune -a
```

Run docker without sudo
```
usermod -aG docker $USER
```

### Docker Hub

```
docker login -u [username]
docker push [image]
```
