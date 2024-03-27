# Installing things with Miniconda on NeSI

> [!NOTE]
> Please see [NeSI's conda instructions](https://support.nesi.org.nz/hc/en-gb/articles/360001580415-Miniconda3) for further details. 

This can be used to install bioconda modules and other tools that require conda environments.

## 1. Initial conda set up

Preferred use of conda on NeSI is typically via Miniconda3.

You will first need to add a script `.condarc` to your home directory. This allows correct set up for your conda environments and channels.

Info in all caps below should be corrected to your user, project ID, and miniconda3 version info.

```bash
  #!/bin/bash

  mkdir -p /nesi/project/PROJECTID/USER/pkgs
  mkdir -p /nesi/project/PROJECTID/USER/CondaEnv

  /nesi/project/PROJECTID/USER/CondaEnv
  cat > /home/USER/.condarc << EOF

  channels:
    - bioconda
    - conda-forge
    - defaults

  pkgs_dirs:
    - /nesi/project/PROJECTID/pkgs

  create_default_packages:
    - setuptools

  envs_dirs:
    - /nesi/project/PROJECTID/CondaEnv

  EOF
```

## 2. Using conda environments for program installation

Load the Miniconda3 module

```bash
module purge
# get latest version
module spider miniconda
module load Miniconda3/VERSION
```

Creating new environments to install tools in.

Here we are specifying the environment name with `-n` and also the version of python required.

We are using the tool mapDamage2 as an example, and following its bioconda installation instructions

```bash
conda create -n mapDamage2 python=3.6

conda activate mapDamage2
# we use the `-c` to tell conda where to look for the installation channels
conda install -c bioconda mapdamage2=2.1.1=pyr36_1
```

When using conda environments within slurm scripts, you may get a `conda init` error, where it says conda won't work in your shell. If so, you need to add: `source /opt/nesi/CS400_centos7_bdw/Miniconda3/VERSION/etc/profile.d/conda.sh` to your script after the `conda activate` command. Make sure to include the correct version of miniconda in the line above. 

## 3. Removing conda environments 

Uninstalling tools in conda is fairly straightforward.

`conda remove --name MYENV --all`
