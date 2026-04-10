# Using submodules

In some cases, e.g. for large Jupyter Books with many contributors, it may be useful to use submodules
to organise the notebooks and other content elements.
A nice example of this is the [C3S training](https://github.com/ecmwf-training/c3s-training)
Jupyter Book which is a collection of notebooks covering many of the C3S data products.
Many of these notebooks were produced by the data providers, and underwent a review process
prior to publication in the main C3S training Jupyter Book.
The submodule setup provided a staging Jupyter Book where notebooks could be published
in a more realistic environment for the reviewers.

:::{note}
It would also be possible to set up a review version of the JupyterBook on a forked repository.
However, we find that controlling a static version of the notebook during the review process
made things run much more smoothly.
:::

## Submodule template

For more details on configuring a repository to be used as a submodule for an upstream
Jupyter Book please see the
[Jupyter Book Submodule Template](https://github.com/ecmwf-training/jupyterbook-submodule-template).

## What is a submodule?

A [git submodule](https://git-scm.com/book/en/v2/Git-Tools-Submodules)
is a standard git tool that lets one Git repository include another repository at a fixed commit.
In practice, this is useful when content is developed and reviewed in a separate
repository, while the parent repository controls exactly which version is published.

When you add a submodule, Git records:

- the submodule URL and branch in `.gitmodules`
- the checked-out submodule **commit** in the parent repository index

:::{note} Updating submodules
As the parent repository tracks the **commit** of the submodule, the parent is not
dynamically updated when changes to the submodule are made.
The parent repository must update its submodule reference to see the changes.
:::


:::{card}
:header: Working with submodules
:link: ../howto/submodules
See the "Working with submodules" how-to guide for some practical examples.
:::