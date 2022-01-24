# Running `jupyter` notebook

This document will guide you to create a `conda` environment and run `jupyter` notebooks in the `adroit` cluster or your own computer. This should be sufficient to do most of the coding projects of APC 523.

`adroit` is Princeton HPC cluster that can be used to run `jupyter` notebook remotely through the new OnDemand web-based platform [MyAdroit](https://myadroit.princeton.edu/).

This guide will mainly use `/bin/bash/` shell and `python3`.

## Setting up `adroit` account
1. If you do not already have `adroit` account, fill in the [registration form](https://forms.rc.princeton.edu/registration/?q=adroit).\
You will receive a helpdesk ticket after filling in the form, please wait until the ticket is resolved and an account is created.
2. If you are not in Princeton network, connect through [VPN](https://informationsecurity.princeton.edu/connecting-to-princeton-n).
3. Make sure you can login to `adroit` through either `ssh` or [MyAdroit](https://myadroit.princeton.edu/).\
In MyAdroit, click on *Clusters* > *Adroit Cluster Shell Access*, or click [here](https://myadroit.princeton.edu/pun/sys/shell/ssh/adroit).
![MyAdroit shell](myadroit_console.png)
4. Load `conda` in the cluster using `module` command.
```
module load anaconda3/2021.11
```
Note that you need to specify the `anaconda` version which you can check through `module avail` command.
5. Test that `conda list` give the list of currently installed packages. You can check the current environment and the `conda` version using `conda info` command.
![Adroit `conda`](adroit_conda.png)

## Setting up `conda` environment
For this course `conda` environment provided in [`APC523.yml`](APC523.yml) should contain relevant packages to do most of the works.

1. Copy the [environment file](APC523.yml) from this site to the location that can be accessed by your terminal.\
You can use the web interface in MyAdroit by clicking *Files* > *Home Directory* or */scratch/network/[netid]*.
![MyAdroit file access](myadroit_files.png)
2. Create the new `conda` environment by invoking the create environment command.
```
conda env create -f [path_to_file]/APC523.yml
```
Wait until the installation is finishes as it might take a while.
3. Test that the environment can be activated through the shell.
```
conda activate APC523
```
4. If you need to remove the environment, you can do so by invoking this command.
```
conda remove --name APC523 --all
```
Verify that the environment is removed using `conda info --envs`.

## Running `jupyter` notebook in cluster
1. Login to [MyAdroit](https://myadroit.princeton.edu/).
2. Click on *Interactive Apps* > *Jupyter* or click [here](https://myadroit.princeton.edu/pun/sys/dashboard/batch_connect/sys/jupyter/session_contexts/new).
![MyAdroit `jupyter`](myadroit_jupyter.png)
3. Fill in the number of hours for reservation (typically <=4 hours, longer duration might take longer in queue) and number of cores (typically 1 as it is hard to parallelize code in `jupyter` notebook). If you are using `jupyterlab` check the option *Use JupyterLab instead of Jupyter Notebook?* then click *Launch*.
![MyAdroit `jupyter` form](myadroit_jupyter_form.png)
4. When the job queue is finished and start running click on the *Connect to Jupyter*. This should open a new tab in your web browser with the typical `jupyter` or `jupyterlab` interface.
![MyAdroit `jupyter` connect](myadroit_jupyter_connect.png)

### Selecting kernel on `jupyter notebook`
Select the kernel from our environment labeled as `APC523` as the Notebook kernel when creating the notebook.\
![`jupyter` new notebook kernel](jupyter_kernel.png)

To change the current notebook kernel, click on *Kernel* > *Change kernel* and select a new kernel from the drop-down list.\
![`jupyter` change current notebook kernel](jupyter_change_kernel.png)

### Selecting kernel on `jupyter lab`
Select the kernel from our environment labeled as `APC523` as the Notebook kernel when creating the notebook.\
![`jupyterlab` new notebook kernel](jupyterlab_kernel.png)

To confirm the current notebook kernel, it is displayed on the top right corner.\
![`jupyterlab` current notebook kernel](jupyterlab_kernel_conf.png)

To change the current notebook kernel, click on the kernel name indicator and select a new kernel from the drop-down list.\
![`jupyterlab` change current notebook kernel](jupyterlab_change_kernel.png)

Note that `jupyterlab` extensions are not currently available through MyAdroit.

## Installing `conda` locally
1. Install the appropriate `conda` package from its [website](https://www.anaconda.com/products/individual).
2. Make sure the instalation is complete and you can use `conda` command in your console.
3. Set up the `conda` environment
4. Activate the environment.
5. Run either `jupyter notebook` or `jupyter lab`

## `jupyterlab` extensions
If you prefer to use `jupyterlab` there are some widgets that can help and should be installed through the terminal after activating the environment. Here I am installing packages related to `matplotlib` plotting module and [`collapsible_headings`](https://github.com/aquirdTurtle/Collapsible_Headings).
```
jupyter labextension install @jupyter-widgets/jupyterlab-manager @aquirdturtle/collapsible_headings
jupyter lab build
```

### `jupyterlab_execute_time` extension
Included in the environment file is the `jupyterlab_execute_time` package. This extension is useful to measure cell execution time.

To enable this in `jupyterlab` insert `{"recordTiming": true}` in *Settings* > *Advanced Settings Editor* > *Notebook* > *User Preferences* or in `[jupyterlab User Settings directory]/@jupyterlab/notebook-extension/tracker.jupyterlab-settings`. Location of the `jupyterlab` user setting file can be retrieved through the command `jupyter lab path`.

For more information about this extension you can check in their [GitHub page](https://github.com/deshaw/jupyterlab-execute-time).

----
[Back to main page](../index.md)
