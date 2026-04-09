# Working with submodules

## Add a submodule to your repository

To add the ECMWF Jupyter Book submodule template under `submodules/` and set it to track
the `main` branch:

```bash
mkdir -p submodules
git submodule add -b main https://github.com/ecmwf-training/jupyterbook-submodule-template submodules/jupyterbook-submodule-template
git submodule update --init --recursive

# commit the new submodule configuration in the parent repository
git add .gitmodules submodules/jupyterbook-submodule-template
git commit -m "Add jupyterbook-submodule-template as a submodule"
```

If someone else clones your repository, they should initialise submodules with:

```bash
git clone --recurse-submodules <your-repo-url>
```

or, if already cloned:

```bash
git submodule update --init --recursive
```

## Updating submodules

The parent repository tracks the the **commit** of the submodule,
therefore the parent is not dynamically updated when changes to the submodule are made.
The parent repository must update it's submodule to see the changes,
often this is just a case of pulling the latest changes to the submodule and then
committing the changes.
For our above example, this would be:

```bash
cd submodules/jupyterbook-submodule-template
git pull

# Check that everything is as intended

cd -
git add submodules/jupyterbook-submodule-template
git commit -m"updated submodules/jupyterbook-submodule-template"
git push
```
