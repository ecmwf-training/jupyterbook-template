# ECMWF Jupyter Book template

This repository is a GitHub **template** for creating and maintaining ECMWF Jupyter Books for learning and documentation resources.

## For authors
Please refer to the [rendered Jupyter Book](https://ecmwf-training.github.io/jupyterbook-template/) for detailed instructions on how to set up and develop your Jupyter Book using this template.

## For developers

Clone the repository and create a conda/mamba environment for building Jupyter Books:
```sh
conda create -y -n jupyter-build -c conda-forge python=3.12
conda activate jupyter-build
conda install "jupyter-book>=2,<3"
```

Then build and render the book
```sh
jupyter book clean
jupyter book build
jupyter book start
```