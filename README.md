# scientific_pythonn_tutorial
 
# Overview
This series of tutorials will introduce python and the python scientific computing (SciPy) stack to R users via ipython and jupyter lab.

# Installation

## HPC
If you're on an HPC cluster then you probably have a python environment ready to load with something like `module load anaconda/3`. This might have everything you need (you can check `conda list` against the requirements in scipy_tutorial_requirements.yml). If not, then you can create a local conda environment as below after loading your HPC cluster's module.

## Local

You need an environment manager. We will use conda (miniconda can be downloaded [here](https://docs.conda.io/en/latest/miniconda.html)), but [mamba](https://mamba.readthedocs.io/en/latest/installation.html) is faster and might be worth your time if you will be using package managers a lot.

Following this, a new conda environment can be created with `conda env create -f scipy_tutorial_requirements.yml`.

# Running notebooks

## HPC

On HPC clusters you will need to start an interactive job, ssh into the compute node, load the python module and activate your environment before starting jupyterlab. Taking SLURM as an example, we start an interactive job with:

```
salloc --job-name=jupyter --time=02:00:00 --nodes=1 --ntasks=1 --tasks-per-node=1 --mem-per-cpu=30G
```

We can then either ssh directly into the node we were allocated or run `srun --pty /bin/bash` to start a bash terminal on the compute node. You can check your node name with `echo "$SLURMD_NODENAME"`. Now load the python module and your conda environment (names will differ for your HPC cluster):

```
module load anaconda/2023.03
source activate
```

Depending on your system, you will either have to run `conda activate env_name` or `source activate env_name`. After this, start a jupyter lab session on port 8889 with

```
jupyter-lab --no-browser --port=8889 --ip=0.0.0.0
```

This will take a while to start up, then will give back some links we can paste into the browser. First though, we have to open a new terminal window and start ssh tunneling. For the Cardiff Hawk HPC cluster, open a new local terminal and type: 

```
ssh -l USERNAME -L 8889:SLURMD_NODENAME:8889 hawklogin.cf.ac.uk
```

Some HPC systems may also be able to use the format:

```
ssh -N -L 8889:SLURMD_NODENAME:8889 username@hpcname.ac.uk
```

Now paste the link given by the jupyterlab session into a new local browser window.

You can now start with the tutorials in /notebooks :)
