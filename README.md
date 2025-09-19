# ECMWF Jupyterbook learning resource template

This repository is a GitHub **template** to facilitate development and maintenance of ECMWF Jupyterbooks used for learning, training and other documentation. It contains example notebooks which provide **best practices** for producing publication quality notebooks.

This template has been designed to be used as a sub-module for a parent repository. Therefore the default branch for this repository is **develop**, and this branch is used to deploy the review/development version of the JupyterBook. The **main** branch is reserved for published content and will be maintained by ECMWF.

The repository includes github-actions which will automatically build a develop version of the Jupyter Book that can be used for review purposes.

## 1. Initial setup

### 1.1 Create your repository

1. Click **Use this template** (green button, top-right).  
2. **Set the repo to *public*** to enable GitHub Pages and Action artifacts.


### 1.2 Update `_config.yml`

Edit the line  
```yaml
repository:
  url: <your-repository-url>
```
to point to the repository that you have just created. This is used as the link to the source in the rendered JupyterBook.

### 1.3 Enable GitHub pages

Go to the "Settings" tab, then navigate to "Pages" on the left-hand menu pane. In the "Build and deployment" section set the source to "GitHub Actions" from the dropdown menu.

> [!WARNING]
> <b>Public repository required for github pages</b> If you did not select "public" when creating the repository you will not be able to enable github pages (unless you are using github enterprise). To make the repository public go to "Settings" -> "General" -> "Danger Zone" -> "Change repository visibility"


To get the link to the rendered Jupyter Book (github pages), go to the "Actions" tab. You will see that the "Initial commit" action failed, this was because the pages were not enabled. You can then click the "Re-run all jobs" buttons in the top right to re-run the actions. This time it should succeed and provide a link to your github pages in the flow diagram.

> [!TIP]
> <b>Optional</b> You can make this link easier to locate in the future by adding it to the "About" section in the right hand panel of the "Code" tab. Click on the settings cog next to about and check the "Use your GitHub Pages website" checkbox.

## 2. Notebook development

### 2.1 Notebook contents & standards (SWUMP)

All training material destined for CDS/ADS/CADS portals must satisfy the SWUMP criteria:

* **S**elf-explanatory: Steps are clearly, correctly and succinctly explained.
* **W**ell structured: Logical flow and aesthetically pleasing layout with a balanced mix of Markdown and code.
* **U**sable: Notebook runs to completion **without errors** and uses only outputs/widgets compatible with JupyterBook.
* **M**eaningful: Provides an authentic, value-adding use-case for CDS/ADS/CADS data.
* **P**roficient: Passes the code-standards tests (see below).

**Code standards tests**
```sh
# install necessary packages
pip install flake8-nb
 
# execute tests with CDS configuration options:
flake8_nb --max-line-length 100 --max-doc-length 100 $NOTEBOOK
```

A review checklist is provided [here](https://confluence.ecmwf.int/pages/viewpage.action?pageId=288335462).

### 2.2 Choose an appropriate template

When developing a notebook please follow the templating guide found in the notebooks provided in this template repository.
Please select a template that is appropriate to the project that you are working on.

### 2.3. Dependancies

The dependancies for the notebooks in this repository should be listed in the `environment.yml` file.
(Please note that the dependancies listed in `ci/requirements.txt` are for the github actions, you should not need to modify these dependancies)

### 2.4. Table of contents

Edit `_toc.yml` to reflect the notebook structure of your JupyterBook.

### 2.5. Best practices

#### Keep notebooks short

Focus on one topic / visualisation / processing routine. Consider separate notebooks if multiple parts or topics are included.

#### Use consistent headings

- Keep headings in separate cells
- Use # for first level headings, ## for second level, and so on. Do not skip a level (e.g. do not follow a 1st level heading with a third level, without a second level in between).

#### Use MyST markdown

For enhanced markdown features (e.g. colored cells, icons), use [MyST markdown](https://mystmd.org/), which is compatible with our JupyterBook setup.

#### Images
- Store notebook-specific images in `./img/.`
- For images reused across repositories (e.g. logos) link to an external URL such as https://climate.copernicus.eu/branding-guidelines#Logolines. Images not already online can be uploaded to a dedicated repository for training hosted at https://sites.ecmwf.int/training/ (please contact [chris.stewart@ecmwf.int](mailto:chris.stewart@ecmwf.int)).
- Use Markdown image syntax: `![<provide alt text>](./img/example.png)`

#### Use of data

Data files should not be stored in the Github repository, but hosted externally and linked to, or downloaded from original source (e.g. CDS/ADS).

#### Notebook metadata

Apply metadata at the notebook level and at the cell level according to a metadata-schema described here: https://github.com/ecmwf-training/jn-metadata-schema.


#### Widgets & interactive output
JupyterBooks run **without a live Python kernel**. Avoid interactive widgets that require a kernel (e.g. many ipywidgets). See the [JupyterBook docs](https://jupyterbook.org/en/stable/interactive/interactive.html#ipywidgets) for a compatibility list.

#### Cross-references & placeholder links
Avoid HTML `<a>` tags without `href` and notebook cross-references built with plain HTML; they render poorly and flood the build with warnings.

#### HTML tags in general
Refrain from using raw HTML—JupyterBook’s config may override or mis-render it. Markdown covers all required formatting.


## 3. Building the JupyterBook

Notebook providers are responsible for ensuring that the GitHub Actions succesfully build and deploy the JupyterBook. It is advisable to test run the build commands and inspect the output locally before pushing to the repository as this will save you time and effort.

### 3.1 Local build (Linux/macOS)

It is recommended that you test the build locally prior to creating your pull request to develop, this will address many of the minor issues you may face and provide you with more readable output. To ensure that you have the same software installed required to build the JupyterBook, and that you are not using any unsupported software packages during a local build, it is recommended that you create an conda-forge environment for building Jupyter Books:

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

### 3.2 GitHub Actions

> [!INFO]
> This template is designed to be used as a sub-module for a parent repository. The JupyterBook build here is intended for review and testing purposes, and hence the actions are associated to the develop branch. If you are using this repostory as a stand-alone JupyterBook you may want to update the default branch and github workflow to use the main branch.

There are two github actions in place for this repository:

#### Build

The **`Build`** action builds the JupyterBook using the same proceedure as local build described below. It is activated when a pull request to the `develop` branch is opened, or when any change is made to the develop branch (e.g. after merging a pull request). A pull request can only be merged into the develop branch if the `Build` action is successful.

#### Deploy

The **`Deploy`** action deploys the build JupyterBook to the GitHub Pages associated with this repository. This action is activated when a change is made to the develop branch, after the build action.

The requirements of the GitHub Actions are listed in `ci/requirements.txt`, do not modify this file. The dependancies of your notebooks should be stored in the `environment.yml` file.
