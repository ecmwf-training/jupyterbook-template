# View your Jupyter Book

Before you deliver your work for review by ECMWF staff, it's worth doing a quick self-check. You can either build the book locally on your computer, or use GitHub to build and host it for you.

## Prerequisites

- [Set up your Jupyter Book](./setup-book.md)


## Option 1: View locally
Create a conda/mamba environment for building Jupyter Books:

```
conda create -y -n jupyter-build -c conda-forge python=3.12
conda activate jupyter-build
conda install jupyter-book
```

With your `jupyter-build` environment activated, run:

```
jupyter book clean  # confirm with "Yes" if prompted
jupyter book start
```

This will start a server that renders your book as a locally-served website. By default, it will be available at [http://localhost:3000/](http://localhost:3000/). Open this URL in your web browser to inspect the rendered book.


## Option 2: View via GitHub pages
Go to the "Settings" tab, then navigate to "Pages" on the left-hand menu pane. In the "Build and deployment" section set the source to "GitHub Actions" from the dropdown menu.

:::{important}
**Public repository required for GitHub pages** If you did not select "public" when creating the repository you will not be able to enable GitHub pages (unless you are using GitHub Enterprise). To make the repository public go to "Settings" -> "General" -> "Danger Zone" -> "Change repository visibility"
:::

To get the link to the rendered Jupyter Book (GitHub pages), go to the "Actions" tab. You will see that the "Initial commit" action failed, this was because the pages were not enabled. You can then click the "Re-run all jobs" buttons in the top right to re-run the actions. This time it should succeed and provide a link to your GitHub pages in the flow diagram.

:::{tip}
**Optional** You can make this link easier to locate in the future by adding it to the "About" section in the right hand panel of the "Code" tab. Click on the settings cog next to about and check the "Use your GitHub Pages website" checkbox.
:::


## Self-review checklist

Before opening a pull request for review, verify that your notebook has filled in (or, where applicable, removed) each of the sections introduced by the template. The checklist below mirrors the manual-review criteria; the [pull request template](../../.github/pull_request_template.md) asks you to link to the section in your deployed book that satisfies each one.

- **Prerequisites** — prior knowledge, related notebooks, required tools/accounts.
- **Target audience** — skill level, role, domain background assumed.
- **Introduction & workflow overview** — context plus an ordered outline of the steps.
- **Learning objectives** — what the reader will be able to do after the notebook.
- **Method and data justification** — why this method, why this dataset, assumptions and limits.
- **Transferability** — what the learner can adapt (region, resolution, variables) and what is fixed.
- **Validation** *(optional)* — sanity checks performed and known limitations.
- **References** — datasets (DOI / persistent ID / stable URL), publications, reused figures.
- **Definitions** *(optional)* — used only when several novel terms are introduced; otherwise define on first use.
- **Figures** — title, axis labels with units, legend, caption with source/attribution; honest scaling; sufficient image quality.
- **Code** — inline comments on non-trivial blocks; docstrings on custom functions; a markdown cell precedes each logical code block.

If a section does not apply to your notebook, remove it (or mark it *not applicable*) rather than leaving the placeholder text in place.
