# Working with submodules

For a thorough demonstration of working with submodules, please refer to the
[git documentation pages](https://git-scm.com/book/en/v2/Git-Tools-Submodules).

## Add a submodule to your repository

The following code snippet will add the ECMWF Jupyter Book submodule template in the
`submodules/` directory and set it to track the `main` branch:

```bash
mkdir -p submodules
git submodule add -b main https://github.com/ecmwf-training/jupyterbook-submodule-template submodules/jupyterbook-submodule-template
git submodule update --init --recursive

# commit the new submodule configuration in the parent repository
git add .gitmodules submodules/jupyterbook-submodule-template
git commit -m "Add jupyterbook-submodule-template as a submodule"
```

## Initialising submodules in a cloned repository

When working with a repository with submodules, the submodules need to be initialised.
To clone and initialise the submodules in a single command, use:

```bash
git clone --recurse-submodules <your-repo-url>
```

or, if the repository has already been cloned, use:

```bash
git submodule update --init --recursive
```

## Updating submodules

The parent repository tracks the **commit** of the submodule,
therefore the parent is not dynamically updated when changes to the submodule are made.
The parent repository must update its submodule to see the changes,
often this is just a case of pulling the latest changes to the submodule and then
committing the changes.
For our above example, this would be:

```bash
cd submodules/jupyterbook-submodule-template
git switch main
git pull

# Check that everything is as intended

cd -
git add submodules/jupyterbook-submodule-template
git commit -m "updated submodules/jupyterbook-submodule-template"
git push
```
