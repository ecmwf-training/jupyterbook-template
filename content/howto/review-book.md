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

Before opening a pull request for review, verify that your notebook has filled in (or, where applicable, removed) each of the sections introduced by the template. The checklist below mirrors the manual-review criteria; the [pull request template](../../.github/pull_request_template.md) asks you to demonstrate that each criterion has been addressed. Where applicable, provide a link to the relevant section in the deployed notebook.

- **Notebook title and introduction** — title, context, purpose, and an ordered outline of the workflow.
- **Learning objectives** — what the reader will be able to do after the notebook.
  - **Target audience** *(optional)* — skill level, role, or domain background assumed.
- **Prepare your environment** — short explanation of the setup steps needed before analysis.
  - **Special prerequisites** *(optional)* — unusual tools, accounts, data access, or setup requirements.
  - **(Install and) Import libraries** — required libraries are installed or imported clearly, with no unused or unexplained setup.
  - **Setup credentials** *(optional)* — credentials are configured without exposing secrets.
  - **Define your data request** *(optional)* — data request parameters are clear, reproducible, and appropriate for the notebook.
- **Main workflow** — the analytical workflow is ordered and easy to follow.
  - **Code sections** — generic placeholders such as `Code section 1` and `Code section 2` have been replaced with meaningful headings; each logical code block is preceded by explanatory markdown.
- **Take home messages** — the notebook closes with the main learning points or practical conclusions.
- **References** — datasets (DOI / persistent ID / stable URL), publications, and reused figures.
- **Glossary** *(optional)* — used only when several novel terms are introduced; otherwise define terms on first use.
- **Licence** *(optional / if applicable)* — licence terms are included where required for data, code, or reused material.

Some manual-review criteria are notebook-wide checks rather than direct notebook sections. Use the pull request template to justify these items when they are not explicit in the notebook text:

- **Method and data choice** — why the selected method and dataset are appropriate for the learning objective.
- **Transferability** — what the learner can safely adapt (for example, region, resolution, variables, or time period) and what is fixed.
- **Validation / limitations** — sanity checks performed, known limitations, or why a separate validation step is not applicable.
- **Figures and visualisations** — titles, axis labels with units, legends, captions, source attribution, readable scaling, and sufficient image quality.
- **Code clarity** — comments on non-trivial blocks, docstrings on custom functions, and readable cell length.

If a section does not apply to your notebook, remove it (or mark it *not applicable*) rather than leaving the placeholder text in place.
