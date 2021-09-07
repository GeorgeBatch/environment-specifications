# Conda Environments and Most Frequent Commands

## Environments

* **standard-ml** includes most common packages for pre-Deep-Learning era
* **medical-cv-cpu** includes most of the `standard-ml` packages. Additionally it includes Deep Learning Computer Vision packages, and packages for working medical images.
* **medical-cv-gpu** has everything from  `medical-cv-cpu`. Additionally it includes `cudatoolkit`.

## Commands

Most commonly used commands are outlined here.

### Create an Environment (from yml)

From: https://stackoverflow.com/questions/48016351/how-to-make-new-anaconda-env-from-yml-file

`conda env create` allows an option `--file` for an environment file:

```{shell}
conda env create --name envname --file=environments.yml
```

### Update an Environment (from yml)

From: https://stackoverflow.com/questions/42352841/how-to-update-an-existing-conda-environment-with-a-yml-file

**Q: How to update an existing Conda environment with a .yml file**

Try using `conda env update`:

```
conda activate myenv
conda env update --file local.yml --prune
```

`--prune` uninstalls dependencies which were removed from `local.yml`, as pointed out in [this answer](https://stackoverflow.com/a/54825300/2261298) by @Blink.

Or without the need to activate the environment (thanks @NumesSanguis):

```
conda env update --name myenv --file local.yml --prune
```

See [Updating an environment](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html?highlight=prune#updating-an-environment) in Conda User Guide.

### Rename an Environment

From: https://stackoverflow.com/questions/42231764/how-can-i-rename-a-conda-environment

**Q: How can I rename a conda environment?**
You can't.

One workaround is to create clone a new environment and then remove the original one.

First, remember to deactivate your current environment. You can do this with the commands:

* `deactivate` on Windows or
* `source` deactivate on Linux.
* `conda`  deactivate on macOS.

Then:

```{shell}
conda create --name new_name --clone old_name
conda remove --name old_name --all # or its alias: conda env remove --name old_name
```

Notice there are several drawbacks of this method:

1. It redownloads packages (you can use `--offline` flag to disable it)
2. Time consumed on copying environment's files
3. Temporary double disk usage

There is an open [issue](https://github.com/conda/conda/issues/3097) requesting this feature.
