Using Bioconda for bioinformatics workflows
===

This is based on Andrew Perry's [tutorial](https://github.com/MonashBioinformaticsPlatform/bioconda-tutorial).

# Conda

The `conda` [package manager](https://en.wikipedia.org/wiki/Package_manager) was originally built by ContinuumIO to support managing dependencies for the [Anaconda Python](https://www.anaconda.com/download/#linux) distribution. It has since been adopted by community projects such as [conda forge](https://conda-forge.org/) and [bioconda](https://bioconda.github.io/) as an easy way to distribute software packages. The bioconda [package repository](https://bioconda.github.io/recipes.html) contains over 8000 bioinformatics packages and is also a crucial component of the [biocontainers](https://biocontainers.pro/) project.

## Advantages to using (bio)conda

* Manages self contained environments, including dependencies. An 'ordinary user' can install it for themselves.

* Large ecosystem of precompiled packages, organized as 'channels' (eg conda-forge, bioconda)

* Language agnostic (not only Python !)

* Creating new packages is straightforward compared with many systems (a recipe composed of a short build.sh and meta.yml).

* Interoperates gracefully with Python virtualenvs and pip.

* Bioconda project imposes quality control on packages with [best practices](http://bioconda.github.io/guidelines.html) and automated testing and package builds.

* Open Source tool (BSD), backed by a company (Continuum Analytics). Some compiled packages in the default 'channel' aren't Open Source.

## How to install conda

1. Get Miniconda (on Linux):

```
    curl -O https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
```
    OR
```
    wget -c https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
```
    On MacOS:
```
    curl -O https://repo.continuum.io/miniconda/Miniconda3-latest-MacOSX-x86_64.sh
 ```
 
2. Run the installer:
```
    bash Miniconda3-latest-Linux-x86_64.sh
```
3. At the prompt agree to the license (type *yes* and press Enter) and install to the default location ($HOME/miniconda3). When asked agree to add the Miniconda python to the path, then log out and back in again.
4. Test that it is installed:
```
$ conda help
usage: conda [-h] [-V] command ...

conda is a tool for managing and deploying applications, environments and packages.

...
```

## Install bioconda
1. Configure conda channels for bioconda
```
conda config --add channels defaults
conda config --add channels conda-forge
conda config --add channels bioconda
```
2. Check your conda config:
```
$ cat ~/.condarc 
channels:
  - defaults
  - conda-forge
  - bioconda
```
    
## Next steps: working with seqtk

1. Install the seqtk package:
```
$ conda install seqtk
Fetching package metadata ...............
Solving package specifications: .

Package plan for installation in environment /Users/perry/miniconda3:

The following NEW packages will be INSTALLED:

    seqtk:     1.2-0            bioconda

The following packages will be UPDATED:

    conda:     4.3.31-py36_0             --> 4.3.33-py36_0 conda-forge

The following packages will be SUPERSEDED by a higher-priority channel:

    conda-env: 2.6.0-h36134e3_0          --> 2.6.0-0       conda-forge

conda-env-2.6. 100% |################################| Time: 0:00:00 395.33 kB/s
seqtk-1.2-0.ta 100% |################################| Time: 0:00:00  63.60 kB/s
conda-4.3.33-p 100% |################################| Time: 0:00:01 279.73 kB/s
```

2. Download some sample data
```
curl https://zenodo.org/record/1324070/files/wt_H3K4me3_read1.fastq.gz >A.fastq.gz
```

3. Make a name list: `echo 'SRR5680996.11626500' >name.lst`
4. Extract a sequence: `seqtk A.fastq.gz name.lst`
5. Reverse complement the sequence: `seqtk A.fastq.gz name.lst|seqtk seq -r`

## Uninstall and re-install in 'environment'

1. Uninstall seqtk: `conda remove -y seqtk`
2. Install in environment: `conda create -n seqtk_env -y seqtk`
3. Activate environment: `source activate seqtk_env`
4. *Freeze* environment: `conda env export >seqtk.yml`