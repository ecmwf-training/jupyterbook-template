# ECMWF Jupyterbook learning resource template

This repository is a github template to facilitate development and maintenance of ECMWF Jupyterbooks used for learning, training and other documentation. It contains a number of template notebooks which provide best practices for producing publication quality notebooks.

This template has been designed to be used as a sub-module for a parent repository. Therefore the default branch for this repository is **develop**, and this branch is used to deploy the review/development version of the JupyterBook. The **main** branch is reserved for published content and will be maintained by ECMWF.

The repository includes github-actions which will automatically build a develop version of the Jupyter Book that can be used for review purposes.

## Initial setup instructions

### Create a repository from this template

A new repository can be created from this by simply selecting the green `Use this template` icon on the top right. The repository should be public to enable all the features required to build the JupyterBook.

### Update the _config.yml

Update the `repository: -> url:` field in the _config.yml to point to the repository that you have just created. This is used as the link to the source in the rendered JupyterBook.

### Enable github pages

Go to the "Settings" tab, then navigate to "Pages" on the left-hand menu pane. In the "Build and deployment" section set the source to "GitHub Actions" from the dropdown menu.

> [!WARNING]
> <b>Public repository required for github pages</b> If you did not select "public" when creating the repository you will not be able to enable github pages (unless you are using github enterprise). To make the repository public go to "Settings" -> "General" -> "Danger Zone" -> "Change repository visibility"


Now go to the "Actions" tab. You will see that the "Initial commit" action failed, this was because the pages were not enabled. You can then click the "Re-run all jobs" buttons in the top right to re-run the actions. This time it should succeed and provide a link to your github pages in the flow diagram.

> [!TIP]
> <b>Optional</b> You can make this link easier to locate in the future by adding it to the "About" section in the right hand panel of the "Code" tab. Click on the settings cog next to about and check the "Use your GitHub Pages website" checkbox.

## Notebook development instructions

## Choose an appropriate template

When developing a notebook please follow the templating guide found in the notebooks provided in this template repository.
Please select a template that is appropriate to the project that you are working on.

## Dependancies

The dependancies for the notebooks in this repository should be listed in the `environment.yml` file.
(Please note that the dependancies listed in `ci/requirements.txt` are for the github actions, you should not need to modify these dependancies)

### Best practices for Jupyter notebooks

#### Keep notebooks short

Focus on one topic / visualisation / processing routine. Consider separate notebooks if multiple parts or topics are included.

#### Keep headings consistent

- Keep headings in separate cells
- Use # for first level headings, ## for second level, and so on. Do not skip a level (e.g. do not follow a 1st level heading with a third level, without a second level in between).

#### Make use of MyST markdown

Use coloured cells, icons, etc. where needed.

#### Use of images

Any images unique to the Jupyter notebook should be stored in the ./img folder in this repository. Any images needed across multiple notebooks in multiple repositories (such as logolines) should be sourced from an external URL (see for example links to ECMWF and Copernicus logos here https://climate.copernicus.eu/branding-guidelines#Logolines). Images not already online can be uploaded to a dedicated repository for training hosted at https://sites.ecmwf.int/training/ (please contact chris.stewart@ecmwf.int).

#### Use of data

Data files should not be stored in the Github repository, but hosted externally and linked to, or downloaded from original source (e.g. CDS/ADS).

#### Notebook metadata

Apply metadata at the notebook level and at the cell level according to a metadata-schema described here: https://github.com/ecmwf-training/jn-metadata-schema.

## Jupyterbook Build instructions

Notebook providers are responsible for ensuring that the github actions succesfully build and deploy the
JupyterBook. It is advisable to test run the build commands and inspect the output locally before pushing
to the repository as this will save you time and effort.

### Building the JupyterBook locally

The following instructions are for Linux and MacOS users.

It is recommended that you test the build locally prior to creating your pull request to develop,
this will address many of the minor issues you may face and provide you with more readable output.
To ensure that you have the same software installed required to build the JupyterBook,
and that you are not using any unsupported software packages during a local build, it is recommended
that you create an conda-forge environment for building Jupyter Books:

```
conda create -y -n JUPYTER-BUILD -c conda-forge python=3.12
conda activate JUPYTER-BUILD
pip install jupyter-book
```

With your JUPYTER-BUILD environment activated the following line will build the jupyterbook locally:

```
rm -rf _build
jupyter-book build --all .
```

This will create all the html files used to create the JupyterBook in the untracked `_build/` folder.
You can open the homepage of this local build with:

```
open _build/html/index.html
```

### GitHub actions

> [!INFO]
> This template is designed to be used as a sub-module for a parent repository. The JupyterBook build here is intended for review and testing purposes, and hence the actions are associated to the develop branch. If you are using this repostory as a stand-alone JupyterBook you may want to update the default branch and github workflow to use the main branch.

There are two github actions in place for this repository:

#### Build

The **`Build`** action builds the JupyterBook using the same proceedure as local build described below.
It is activated when a pull request to the `develop` branch is opened, or when any change is made to the 
develop branch (e.g. after merging a pull request). A pull request can only be merged
into the develop branch if the `Build` action is successful.

#### Deploy

The **`Deploy`** action deploys the build JupyterBook to the github pages associated with this repository.
This action is activated when a change is made to the develop branch, after the build action.

The requirements of the github actions are listed in `ci/requirements.txt`, do not modify this file.
The dependancies of your notebooks should be stored in the `environment.yml` file.

## Troubleshooting notes

1. Multiple Level 1 Headers (#) in a notebook will break various aspects of the JupyterBook build.
2. JupyterBooks do not have a running python kernel, threrefore they are not compatible with interactive widgets which require a running kernel, e.g. a number of ipywidgets, as documented here: https://jupyterbook.org/en/stable/interactive/interactive.html?highlight=widgets#ipywidgets
3. Any additional images included in the notebook should be added using markdown hyperlink syntax, html syntax does not work with our jupyter-books. e.g.: `![](.images.png)`
4. Please avoid using placeholder hyperlinks using (the HTML <a> tag without a href provided) and within notebook cross-references (links between sections of the notebook). Due to platform differences they are not rendered correctly on JupyterBook pages and causes many compilation warnings and errors. This means it is much harder for us to identify real issues in the notebook, slowing down the integration process.
5. Please refrain from using HTML tags in general as they often intefere with the HTML config that JupyterBook builds and do not necessarily produce the intended effect when deployed in different environments. Markdown should offer all the text formatting required for the purposes of these traning notebooks.
