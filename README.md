[![PyPI version](https://badge.fury.io/py/bool-to-int8-ray.svg)](https://badge.fury.io/py/bool-to-int8-ray)
[![PyPi downloads](https://img.shields.io/pypi/dm/bool-to-int8-ray)](https://img.shields.io/pypi/dm/bool-to-int8-ray)
[![DOI](https://zenodo.org/badge/638482784.svg)](https://zenodo.org/badge/latestdoi/638482784)


# bool-to-int8-ray: Boolean Vectors to 8-bit Integer Vector Serialization with Ray.io
The software serializes a series of binary vectors, e.g., 0001010101..., to 8-bit integer numbers, and deserializes too. The python code is parallelized for CPUs with Ray.io.

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
The `bool-to-int8-ray` [git repo](http://github.com/ulf1/bool-to-int8-ray) is available as [PyPi package](https://pypi.org/project/bool-to-int8-ray)

```sh
pip install bool-to-int8-ray
pip install git+ssh://git@github.com/ulf1/bool-to-int8-ray.git
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
Please [open an issue](https://github.com/ulf1/bool-to-int8-ray/issues/new) for support.


### Contributing
Please contribute using [Github Flow](https://guides.github.com/introduction/flow/). Create a branch, add commits, and [open a pull request](https://github.com/ulf1/bool-to-int8-ray/compare/).

### Acknowledgements
The "Evidence" project was funded by the Deutsche Forschungsgemeinschaft (DFG, German Research Foundation) - [433249742](https://gepris.dfg.de/gepris/projekt/433249742) (GU 798/27-1; GE 1119/11-1).

### Maintenance
- till 31.Aug.2023 (v0.1.1) the code repository was maintained within the DFG project [433249742](https://gepris.dfg.de/gepris/projekt/433249742)
- since 01.Sep.2023 (v0.2.0) the code repository is maintained by [@ulf1](https://github.com/ulf1).
