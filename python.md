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
