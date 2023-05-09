[![PyPI version](https://badge.fury.io/py/bool-to-int8-ray.svg)](https://badge.fury.io/py/bool-to-int8-ray)
[![PyPi downloads](https://img.shields.io/pypi/dm/bool-to-int8-ray)](https://img.shields.io/pypi/dm/bool-to-int8-ray)

# bool-to-int8-ray
bool to int8 serialization with ray.io

## Installation

```
pip install bool-to-int8-ray
```

## Usage

```sh
export B2I8_PCT_CPU=0.6
```

```py
from bool_to_int8_ray import bool_to_int8_batch, int8_to_bool_batch
import numpy as np

# given lists of binary hashes
hashvalues = np.array([
    [1, 0, 1, 0, 1, 1, 0, 0],
    [1, 1, 0, 0, 0, 0, 0, 1]
])
# convert to list of int8 values
serialized = bool_to_int8_batch(hashvalues)
# convert back
deserialized = int8_to_bool_batch(serialized)
```

## Speed Test

```sh
source .venv/bin/activate
export B2I8_PCT_CPU=0.6
python test/speedtest.py
```

Results
```
 4.776991 -- numpy version, hash to int8
 6.031101 -- numpy version, int8 to hash
 2.308446 -- ray.io version, hash to int8
 3.023865 -- ray.io version, int8 to hash
```

## Appendix

### Installation
The `bool-to-int8-ray` [git repo](http://github.com/satzbeleg/bool-to-int8-ray) is available as [PyPi package](https://pypi.org/project/bool-to-int8-ray)

```sh
pip install bool-to-int8-ray
pip install git+ssh://git@github.com/satzbeleg/bool-to-int8-ray.git
```

### Install a virtual environment

```sh
python3 -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt --no-cache-dir
pip install -r requirements-dev.txt --no-cache-dir
```

(If your git repo is stored in a folder with whitespaces, then don't use the subfolder `.venv`. Use an absolute path without whitespaces.)

### Python commands

* Jupyter for the examples: `jupyter lab`
* Check syntax: `flake8 --ignore=F401 --exclude=$(grep -v '^#' .gitignore | xargs | sed -e 's/ /,/g')`
* Run Unit Tests: `PYTHONPATH=. pytest`
* Run Speed Test: `python test/speedtest.py`

Publish

```sh
# pandoc README.md --from markdown --to rst -s -o README.rst
python setup.py sdist 
twine upload -r pypi dist/*
```

### Clean up 

```sh
find . -type f -name "*.pyc" | xargs rm
find . -type d -name "__pycache__" | xargs rm -r
rm -r .pytest_cache
rm -r .venv
```


### Support
Please [open an issue](https://github.com/satzbeleg/bool-to-int8-ray/issues/new) for support.


### Contributing
Please contribute using [Github Flow](https://guides.github.com/introduction/flow/). Create a branch, add commits, and [open a pull request](https://github.com/satzbeleg/bool-to-int8-ray/compare/).
