# Quality assurance

:::{important}
We're currently in the process of improving our quality assurance guidelines for notebook authors. Below you'll only find a minimal set of checks. Also, please refer to the [review checklist](https://confluence.ecmwf.int/pages/viewpage.action?pageId=288335462) (restricted access, for authors only) to ensure your content meets all required standards.
:::


## Python dependencies

Ensure that the Python dependencies required to run the notebook(s) are included in the `environment.yml` file.

## Coding standards

Ensure that all code in the notebook(s) adheres to the ECMWF coding standards for Python.

To do so, activate your `jupyter-build` environment:

```sh
conda activate jupyter-build
```

Then, install the `flake8-nb` package and run the code standards tests on your notebook (replace `$NOTEBOOK` with the path to your notebook file):

```sh
# install necessary packages
conda install flake8-nb
 
# execute tests with CDS configuration options:
flake8_nb --max-line-length 100 --max-doc-length 100 $NOTEBOOK
```

