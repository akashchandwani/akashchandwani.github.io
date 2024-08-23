---
title: "Setting Up Essential Data Science Tools"
date: 2024-08-23T22:02:07+05:30
draft: false
tags: ["setup", "python", "anaconda", "jupyter-notebooks", "data-science"]
---

Getting started with data science involves setting up a few key tools. In this guide, we'll walk through the installation of:

1. Python
2. Anaconda
3. Jupyter Notebooks

# 1. Python Installation

Before installing a specific version of Python, it's good practice to check if you already have it installed and which version you're using.


## Check Existing Python Installation

To find the path of the current Python executable, use:

```
which python
```

To check the version of Python installed, run:

```
python -V
```

## Using `pyenv` for Python Version Management
To manage different versions of Python, we'll use [pyenv](https://github.com/pyenv). pyenv simplifies the process of installing and switching between multiple Python versions.

## Install `pyenv`

You can install pyenv using Homebrew. Run the following commands:

```
brew update
brew install pyenv
```

## Manage Python Versions with `pyenv`

Here are some useful `pyenv` commands:

1. List available python versions:
```
pyenv install -l
```

2. Install a specific Python version:
```
pyenv install 3.10
```

3. Set a global Python version:
```
pyenv global 3.10
```

4. Set a local Python version for a directory:
```
pyenv local 3.10
```

5. Upgrade `pyenv`
```
brew upgrade pyenv
```

# 2. Installing Anaconda

Anaconda is a popular distribution for data science that simplifies package management and deployment.

## Install Anaconda:

1. Visit the Anaconda [website](https://www.anaconda.com/download) and download the installer for your operating system.
2. Once the download is complete, run the installer and follow the on-screen instructions to complete the installation.

# 3. Installing Jupyter Notebooks

Jupyter Notebooks are an essential tool for data analysis and visualization.

## Install Jupyter Lab

```
pip install jupyterlab
```

## Launch Jupyter Lab

After installation, start Jupyter Lab with:

```
jupyter lab
```

This command will open Jupyter Lab in your web browser, where you can create and manage notebooks.

# Summary

By following these steps, you’ll have Python, Anaconda, and Jupyter Lab set up and ready for your data science projects. Each tool plays a crucial role in developing and managing your data science workflows efficiently.
