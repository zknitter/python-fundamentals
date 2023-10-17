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
<env-name>/Scripts/activate
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

**TODO: note importance of `requirements.txt`**
