Anaconda is an open-source distribution of Python. It comes with the Python interpreter, a package manager and various packages related do data science.

## Installing

### Anaconda
Download Anaconda executable and follow the instructions to install Anaconda in your system.

https://www.anaconda.com/download

### Miniconda
Miniconda is a minimal installation of Conda + Python + other userful packages (pip, zlib ...).

https://docs.conda.io/projects/miniconda/en/latest/#

## Conda
Conda is the main Anaconda package manager.

* `conda create --name environment-name python=version`: create a new environment
* `conda activate environment-name`: activate the indicated environment
* `conda deactivate`: deactivate the current environment
* `conda env list`: list environments
* `conda remove -n environment-name --all`: delete environment-name

* `conda install package-name`: install package-name
* `conda env export > filename.yml`: export current environment
* `conda env create --file filename.yml`: create new environment from filename.yml
