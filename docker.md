## Docker

Remove all images and containers 
```
sudo docker system prune -a
```

Container in interactive mode
```
sudo docker run -it [image] [command]
sudo docker run -it python bash
```

Build a image
```
sudo docker build . -t [domain/project]
sudo docker build . -t [image id]
sudo docker build . -t campusboard/site
```

Run
```
sudo docker run -it -p [local port]:[container port] [image id]
sudo docker run -it -p 8080:5000 campusboard/site
```

List images
```
sudo docker image ls
```

List all containers
```
sudo docker ps -a
```

Stop a container
```
docker stop [container id]
```

Copy files to container
```
sudo docker [files on local machine (origin)] [image id]:[files to container (destiny)]
sudo docker cp ./pipeline campusboard/pipeline:./
```

Dockerfile
```
FROM [image base]
RUN [commands]
WORKDIR [path to work dir]
COPY [files on local machine (origin)] [files to container (destiny)]
EXPOSE [port]
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
