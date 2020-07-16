# Cheat Sheet

Because I have a bad memory...

## Git

Configuration
```
git config --global user.name "[name]"
git config --global user.email "[email address]"
git config --global color.ui true
```

Initialize a local repositpory
```
git init
```

Clone a repository
```
git clone git@github.com:tsuhadaniel/cheatsheet.git
git clone https://github.com/tsuhadaniel/cheatsheet.git
```

Show modified files
```
git status
```

Add files to staging
```
git add [file]
git add --all
```

Commit
```
git commit -m "[message]"
git commit --amend -m "[message]"
```

Undo commit
```
git reset --soft HEAD^
```

Reset staging area
```
git reset
```

Reset staging area and overwrites all changes
```
git reset --hard
```

Go to/Create a branch
```
git checkout [branch name]
```

Update branch
```
git pull
git pull [remote branch] [local branch]
```

Delete branch
```
git branch -d [branch name]
```

Update local repository
```
git pull --rebase origin master
```

Update remote branch
```
git push origin 
```

Add remote server
```
git remote add origin git@github.com:tsuhadaniel/cheatsheet.git
```

## Python

Run tests
```
python -m unittest
```

Run specific test
```
python -m unittest [dir].[file].[class].[method]
python -m unittest test.test_filters.TestButterworth.test_shift
```

## Conda

Install on Docker containner
```
FROM python

RUN curl https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh --output miniconda.sh \
    && bash miniconda.sh -b -p $HOME/miniconda
    
RUN eval "$($HOME/miniconda/bin/conda shell.bash hook)" \
    && conda init \
    && conda create --name [env name] -y \
    && conda activate [env name] \
    && conda install -y [package]

EXPOSE [port (important to AWS EBS)]

CMD eval "$($HOME/miniconda/bin/conda shell.bash hook)" \
    && conda activate [env name] \
    && python [main file]
```

Create environment
```
conda create --name [name] python=[version - optional]
```

Delete environment
```
conda env remove --name [name]
```

List environments
```
conda env list
```

Save environment to a text file
```
conda list --explicit > [file name].txt
```

Create environment from a text file
```
conda env create --file [file name].txt
```

Activate environment
```
conda activate [name]
```

Install packages
```
conda install -y [package name]
```

Update a package in the current environment
```
conda update [package name]
```

Jupyter
```
jupyter-notebook
jupyter-lab
```

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
