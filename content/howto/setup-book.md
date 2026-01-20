# Set up your Jupyter Book

This guide walks you through the minimum setup to create your own Jupyter Book based from this ECMWF Jupyter Book template.

## Clone the repository

To clone this template repository and create your own Jupyter Book project, follow these steps:

1. Open the [template repository](https://github.com/ecmwf-training/jupyterbook-template) on GitHub. 
2. Click **Use this template** (green button, top-right).
3. Choose a repository name and owner.

:::{important}
Set the repo to *public* to enable GitHub Pages and Action artifacts.
:::


## Update `myst.yml`
 
Update the project metadata to reflect your project details. In particular, update the `github` and `thebe.binder.repo` fields with your repository name:

```yaml
project:
  title: <book title>  # replace <book title> with your project title
  # ...
  github: ecmwf-training/<your-repo-name>  # replace with your repository name
  # ...
  thebe:
    binder:
      repo: ecmwf-training/<your-repo-name>  # replace with your repository name (same as above)
```

## Choose branding (optional)

By default, the template uses Copernicus Climate Change Service (C3S) branding. You can easily switch to ECMWF or Copernicus Atmosphere Monitoring Service (CAMS) branding instead:

1. Open the `myst.yml` file in the root of your Jupyter Book repository.
2. Change the `extends` line to select the desired branding configuration:

::::{tab-set}
:::{tab-item} ECMWF
:sync: ecmwf
```yaml
extends:
  - branding/ecmwf.yml
```
:::
:::{tab-item} C3S
:sync: c3s
```yaml
extends:
  - branding/c3s.yml
```
:::
:::{tab-item} CAMS
:sync: cams
```yaml
extends:
  - branding/cams.yml
```
::::

That is all that is required.


## Next steps
- Remove the example content and start adding your own pages and notebooks, following the [best practices](../reference/best-practices.md).
- Before submitting your work for ECMWF review, review your Jupyter Book [yourself](./review-book.md) by following the [quality assurance guidelines](../reference/quality-assurance.md).

That's it! You're now ready to start drafting your book.