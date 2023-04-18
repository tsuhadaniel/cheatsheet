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

## Object Orientation

```python
class ClassName:

    static_value = 123

    # Constructor
    def __init__(self, param_1, param_2):
        self.__param_1 = param_1 # Private attribute
        self.param_2 = param_2 # Public attrubute

    def public_method(self):
        pass

    def __private_method(self):
        pass

    # Get [some_var = instance.param_1]
    @property
    def param_1(self):
        return self.__param_1

    # Set [instance.param_1 = 'some_value']
    @param_1.setter 
    def param_1(self, param_1):
        self.__param_1 = param_1

    @staticmethod
    def static_method():
        return 'abc'
```
