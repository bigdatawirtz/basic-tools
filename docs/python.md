

## Anaconda
Anaconda is an open-source distribution of Python. It comes with the Python interpreter, a package manager and various packages related do data science.

### Installing

#### Anaconda
Download Anaconda executable and follow the instructions to install Anaconda in your system.

https://www.anaconda.com/download

#### Miniconda
Miniconda is a minimal installation of Conda + Python + other userful packages (pip, zlib ...).

[Install instructions](https://docs.conda.io/projects/miniconda/en/latest/#)

Quick Install

```
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash ~/Miniconda3-latest-Linux-x86_64.sh
```

Manual installation
```
mkdir -p ~/miniconda3
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh
bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
rm ~/miniconda3/miniconda.sh
```
Configure conda autoload:

`~/miniconda3/bin/conda init bash`

### Conda
Conda is the main Anaconda package manager.

* `conda create --name environment-name python=version`: create a new environment
* `conda activate environment-name`: activate the indicated environment
* `conda deactivate`: deactivate the current environment
* `conda env list`: list environments
* `conda remove -n environment-name --all`: delete environment-name
* `conda install package-name`: install package-name
* `conda env export > filename.yml`: export current environment
* `conda env create --file filename.yml`: create new environment from filename.yml

### PIP
pip is the package installer for Python. It allows you to install, update, and manage Python packages and libraries from the Python Package Index (PyPI).

* `conda install pip`: install pip if you are in a fresh conda environment
* `pip install package-name`: install the selected package in the current environment
* `pip uninstall package-name`: uninstall the selected package from the current environment

### New Project sample
Imagine that you start a new project with the following requirements:

* python interpreter 3.8
* pyjokes library

You can create a new environment, activate it, install pip, install the required libraries with pip and then execute the script.

```
conda create --name newproject python=3.8
conda activate newproject
conda install pip
pip install pyjokes
```