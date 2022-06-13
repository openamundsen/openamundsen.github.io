---
layout: default
title: Installation
parent: Documentation
nav_order: 1
permalink: /doc/installation
---

# Installation

openAMUNDSEN is a Python (3.7+) package and compatible with all major platforms (Linux, macOS,
Windows) and architectures.

To help keep its dependencies separated from other Python packages installed on your system, we
recommend to install it either from within a conda environment (if you are using the
[conda](https://docs.conda.io/en/latest/) package manager) or a standard Python [virtual
environment](https://docs.python.org/3/tutorial/venv.html).

## Using conda

When using conda, the recommended steps to install openAMUNDSEN are:

1. Install [Miniconda](https://docs.conda.io/en/latest/miniconda.html) (recommended) or
   [Anaconda](https://www.anaconda.com/products/individual#Downloads) by downloading and executing
   the installer for your operating system and architecture.
2. From the terminal, create a conda environment for openAMUNDSEN by running

   `conda create --name openamundsen`
3. Activate the environment by running

   `conda activate openamundsen`
4. Install openAMUNDSEN by running

   `conda install --channel=conda-forge openamundsen`

   If you want to use the LiveView window during model runs, additionally install the packages matplotlib and PyQt5 by running

   `conda install --channel=conda-forge matplotlib`

   and

   `pip install PyQt5`



## Using virtualenv

If you want to install openAMUNDSEN in a virtual environment instead:

1. Create a virtualenv in the current working directory by running

   `python3 -m venv openamundsen`

2. Activate the environment by running

   `source openamundsen/bin/activate`

3. Install openAMUNDSEN by running

   `pip install openamundsen`

   If you want to use the LiveView window during model runs, additionally install the packages matplotlib and PyQt5 by running

   `pip install matplotlib PyQt5`
