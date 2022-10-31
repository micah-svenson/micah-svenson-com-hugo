---
title: "Dead Simple Method for Managing Python Virtual Environments"
date: 2022-10-11T19:28:44-06:00
draft: false
tags: Python
---

While there are many tools for managing python virtual environments, sometimes you just need something portable and dead simple. 

## The Method

1. Use Python's venv module directly
2. Create virtual environment directories in your project's root -- *always* call it `env/`.
3. (Optional) add an alias to make virtual environment activation more convenient.
4. Create, activate, deactivate, and delete environments to you hearts content.

## The Commands You Need
*Disclaimer: These commands work on linux and mac, but will require modifications for Windows*

1. Create a virtual environment folder in the current directory
```shell
python3 -m venv env
```
2. Activate a virtual environment in the current directory(manually)
```shell
$ source env/bin/activate
```
4. Deactivate the currently activated virtual environment
```shell
$ deactivate
```
3. (Optional) Activate a virtual environment in the current directory with an alias. See [Configuration](#configuration).
```shell
$ pyenv
```
## Examples

### Creating a new virtual environment
```shell
# navigate to a project root folder
cd ~/new-project

# create the environment
# Note: the python version invoked here will be the same version available in the virtual environment
python3 -m venv env

# activate the environment
pyenv

# or
source ./env/bin/activate

```

### Moving Between Projects With Different Environments
I have two projects -- project1 and project2. I have already created an environment in the root of project1, activated it, and added some packages. Now, I need to move to project2, which has an entirely different set of dependencies, and activate the environment.

```shell
# Navigate to a project folder
cd ~/project1

# activate project 1 virtual environment
pyenv

# Do some work in project 1
...

# Move to project2 directory
cd ~/project2

# activate project2 virtual environment. (previously active environment will be deactivated first.)
pyenv

# Do some work in project 2
...

# Deactivate the current environment and move to the base environment
deactivate

```

### Deleting an environment
```shell
# navigate to project root
cd ~/project1

# delete the env folder
rm -rf env
```

## Configuration
Add an alias to your terminal configuration to make activate virtual environments more convenient. The example below will work for linux.

```shell
$ echo "alias pyenv=source ./env/bin/activate" >> ~/.bashrc
$ source ~/.bashrc
```

After adding this alias, typing the `pyenv` command will activate a virtual environment that is located in the current directoy and called `env`

## Why Choose This Method?

* No external package dependencies to install and configure
* Easier to keep track of which python environment should be associated with a given project
* Only requires a few commands
* The virtual environments are visible within the project and not hidden away
* Encourages creating new environments to isolate any project rather than reusing environments or just trashing your base environment


## Why Not?
* You aren't interested in dealing with nitty-gritty details and want a set it and forget it solution.
* You enjoy constantly reconfiguring your environment when moving between computers or servers
* You have a large project that would benefit from a more robust tool such as [poetry](https://python-poetry.org)

