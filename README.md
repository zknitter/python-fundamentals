# Python Fundamentals

This repository was originally cloned from [python-fundamentals](https://github.com/fbaptiste/python-fundamentals), created by Fred Baptiste. I have replaced the original README file with my own notes taken alongside the Python Fundamentals lessons.

# Course Background

This course covers the basics of Python from the ground up, which I am hoping to use as a means of reviewing and revising my own knowledge and understanding of Python 3 in furtherance of my own learning goals.

# Resources

- Course page: https://www.udemy.com/course/python3-fundamentals/
- Course repo: https://github.com/fbaptiste/python-fundamentals

# Installation Notes

- The canonical version of Python is CPython, but there are other implementations, including a version that integrates with .NET called IronPython. (This appears to rely on compilation to an intermediate language to transpile code to C# and .NET.)
- Multiple versions of Python can be installed simultaneously ("side-by-side") on a computer, making it possible to alternate between versions when authoring/running code.
- Newer versions of Python (e.g. 3.6 and later) include a **Python Launcher**, which allows one to easily view which versions of Python are installed alongside one another on a machine.
	- To invoke the Python launcher, open a command prompt and type `py --list`. This will list all the installations of Python on the relevant machine.
	- Calling `py --list-paths` shows the full paths to the installations.
	- A python session can be opened using `py` (a full call to `python` is not necessary!), and different versions can even be called using the same command, as in `py -3.8` to open a shell in version 3.8.

# Reproducible Workflow

As an overview, the steps for a reproducible workflow are:
1. Create a new virtual environment
2. Activate the virtual environment
3. Create a `requirements.txt` file with 3rd-party packages
4. Call `pip install -r requirements.txt` within the environment to install packages

The following sections in this README describe these steps and how they contribute to reproducibility.


# Virtual Environments

In order to make code reproducible, all development in Python should take place within **virtual environments**.

Virtual environments allow one to specify all dependencies associated with a Python project - including the version of Python used - and package those dependencies alongside the code for the project itself.


## Creating a Virtual Environment

To create a virtual environment in a directory `dirname`, open a terminal and call:
```bash
py -3.10 -m venv dirname/<env-name>
```
This will use the Python Launcher to run the Python module (`-m`) entitled `venv` to create a virtual environment in the working directory with Python version 3.10, giving it the name `<env-name>`.


## Activating/Deactivating a Virtual Environment

Once the virtual environment exists, *it needs to be activated* in order to maintain dependencies and reproducibility. When a virtual environment is activated, it acts as if the PATH has been modified and ensures that shell calls to `python` run against the version of the language installed in the virtual environment.

On Windows, a virtual environment is activated using the following shell command:
```bash
dirname/<env-name>/Scripts/activate
```
This command runs the `activate.bat` file, which activates the environment. 

So long as the virtual environment is active, there will be an indication in the command prompt based upon the parenthesis around the environment name `(env-name)` before the cursor.

Virtual environments can be deactivated by calling:
```bash
deactivate
```

Because this command is being called from within an active virtual environment, it does not require any path specification.


## Installing Packages in a Virtual Environment

Third-party packages are installed with the **Package Installer for Python (`pip`)**. `pip` uses the **Python Package Index (https://pypi.org)**.

As a general rule to aid reproducibility, **packages installed using `pip` should specify a version number**. This is also referred to as "pinning" the version of the package.

To install packages within a virtual environment, call:
```bash
dirname/<env-name>/Scripts/activate    # activate virtual environment
pip install package_name==1.0.0        # installs package_name version 1.0.0 in venv
```


### requirements.txt

While the approach above works for iterating on a script or notebook, it is better to use the conventional `requirements.txt` file to specify required packages and their versions.

The `requirements.txt` file is a standard means of designating the packages (and their versions) referenced in a script, module, package, etc. This file is simply a text file named `requirements.txt` formatted as follows:
```txt
<package_name>==<version>
<package_name>==<version>
```
For example:
```
numpy==1.18.1
pandas==1.1.4
matplotlib==3.3.3
```
Importantly, there is no requirement that this file be called `requirements.txt`, but this is a standard convention and there is no good reason to depart from it.

Using a `requirements.txt` file greatly facilitates reproducibility by:
1. specifying a single, understandable location to identify all relevant dependencies, and
2. enabling installation of all dependencies via a simple command. 

**To install all required packages from `requirements.txt`, call:**
```bash
(venv)> pip install -r requirements.txt
```

PIP also includes some useful commands to iteratively define requirements. For example, calling `pip freeze` within a virtual environment lists all of packages installed in the environment as well as their versions. Modifying this, one can write the required packages to a file using:
```bash
(venv)> pip freeze > requirements.txt
```

# How Python Runs

Python is *both* a compiler and an interpreter. Python code is comipled to bytecode and then interpreted by a virtual machine before running with the operating system.

The basic processing steps are as follows:
1. Python code is executed
2. Python compiler performs checks on code (e.g. for syntax errors)
3. Python compiler compiles checked code to bytecode
4. Virtual machine interprets bytecode for operating system (OS-specific)
5. Operating system executes interpreted bytecode
6. Operating system returns results to virtual machine

Python code can be run in two different ways, much like R: in **interactive mode** (REPL) and in **script mode** (batch).

## Interactive Mode

To run Python interactively, type `python` in the command line (from within a virtual environment). This opens a basic read-evaluate-print loop (REPL).

```bash
python # open python REPL
>>> # type python code here
```

This interface is not very useful on its own, in part because everything is ephemeral - hence the creation of Jupyter notebook and other frameworks.

## Script Mode

To run Python scripts, the code should be saved in (at least) one `.py` file and run using:

```bash
python <app_name>.py
```

This approach is much more organized than notebooks and one-off script files because it allows for more sophisticated structures, automated testing, and design patterns.

# Jupyter Notebooks

[Jupyter notebooks](https://docs.jupyter.org/en/latest/) are one of the most popular ways to experiment with Python and develop initial versions of analysis scripts. One of the main advantages of Jupyter notebooks is that they allow for documentation and REPL-style code to exist (and run!) within a single document.

To use Jupyter notebooks, one must first have the `notebook` Python package installed in the relevant virtual environment.

```bash
<env-name>/Scripts/activate 	# activate virtual environment
(env-name)> pip install notebook
```

Once installed, Jupyter can be run in the working directory(`.`) using:

```bash
(env-name)> jupyter notebook . 	# opens browser window
```

This command opens a Web browser window after activating a local server to run the notebook files. Within the browser window, you can create new notebook files, browse existing files, run notebooks, and much more.

For most purposes, **the primary value in using Jupyter notebooks is to streamline interactive, exploratory data analysis** which can then be both documented (using Markdown syntax), versioned, and exported (in a variety of formats, including static Markdown files). This is obviously very similar to R markdown, though with several tooling limitations.

