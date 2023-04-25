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

Class
```python
class ClassName(SuperClass1, SuperClass2):

    class_attribute = 123

    # Constructor
    def __init__(self, param_1, param_2, param_3):
        super().__init__('super_class_1_parameters') # SuperClass1 constructor
        super().__init__('super_class_2_parameters') # SuperClass2 constructor
        self.__param_1 = param_1 # Private attribute (name mangling)
        self._param_2 = param_2 # Private attribute (convetion)
        self.param_3 = param_3 # Public attribute

    def public_method(self):
        pass

    def __private_method(self): # Name mangling
        pass

    # Get [some_var = instance.param_1]
    @property
    def param_1(self):
        return self.__param_1

    # Set [instance.param_1 = 'some_value']
    @param_1.setter 
    def param_1(self, param_1):
        self.__param_1 = param_1

    def get_class_attribute(self):
        return __class__.class_attribute

    @classmethod # Can access class and instances
    def class_method(cls): # cls is equivalent to self but for classes 
        return f'Class attribute value: {cls.class_attribute}'

    @staticmethod # Cannot access class and instances
    def static_method(): # no self
        return 'abc'
```

Abstract class (can be used as interface)
```python
from abc import ABCMeta, abstractmethod

class AbstractClass(metaclass = ABCMeta):

    @abstractmethod
    def method(self):
        pass
```

Mixins
```python
import json

class JSONSerializableMixin:
    def to_json(self):
        return json.dumps(self.__dict__)
    
    @classmethod
    def from_json(cls, json_str):
        obj_dict = json.loads(json_str)
        return cls(**obj_dict)

class Person(JSONSerializableMixin):
    def __init__(self, name, age):
        self.name = name
        self.age = age

person = Person("Alice", 30)
json_str = person.to_json()
print(json_str)  # {"name": "Alice", "age": 30}

new_person = Person.from_json(json_str)
print(new_person.name)  # Alice
print(new_person.age)  # 30
```
