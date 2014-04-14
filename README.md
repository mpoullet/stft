Skeleton
========

A skeleton for scientific Python projects.



Purpose
-------

Getting started with a new language can be tricky. There are many tools and
workflows that need to be learned in order to be able to fully utilize the
language.

Secondly, to make new projects useful to other people, a certain project layout
style should be followed as closely as possible.

This skeleton is there to help create a new project using the Python and SciPy
software stack. It uses popular tools to install and separate single projects
and their dependencies from other projects.



Installation
------------

### Virtual Environment

The following installation instructions assume that you have a so-called virtual
environment set up. To create a new virtual environment named `NAME` you have to
run the following:

    virtualenv --system-site-packages NAME

To activate the environment you do:

    cd NAME
    source bin/activate

Deactivating the environment is done by running:

    deactivate

These environments ensure that you can have several versions of both the Python
interpreter and the installed libraries installed side by side without them
interfering with each other.

It is recommended to create a virtualenv for every single project you create.

It is recommended to **never install dependencies system-wide**, e.g. outside a
virtual environment and using `sudo pip install` or `sudo python setup.py`.

The only exception are libraries that can be installed using an OS-installer like
`apt-get` or `pacman` etc. Usually libraries like NumPy, SciPy and Matplotlib
are installed system-wide and will not be installed separately in each single
virtual environment.



### End-User Installation

This section is for end-users who want to install and use the software in
their own projects. Copy/clone the source files in your virtual environment:

    git clone git@work.audiolabs.uni-erlangen.de:nils/python-skeleton.git
    cd python-skeleton

install the library and all its dependencies:

    python setup.py install

You may now delete the source-folder again:

    cd ..
    rm -rf python-skeleton




### Development

This section is for users who want to do development on the package that
contains this README file. Copy/clone the source files into your virtual
environment:

    git clone git@work.audiolabs.uni-erlangen.de:nils/python-skeleton.git
    cd python-skeleton

install all dependencies so you can start developing:

    python setup.py develop



#### Custom data for development

Sometimes the data required for developing the library can't be included in the 
repository itself for various reasons. To still fetch the data for development,
the `python setup.py develop` command has been extended using the class
`DevelopCommandProxy` in `setup.py`.

In the `run()` method of that class there are two exemplary calls to
`urllib.urlretrieve()` that each retrieve a remote file and save it inside the
project file structure.

Use these examples to automatically download test- and development data.

These files will not be downloaded if a user is merely installing the library
by using `python setup.py install` or `pip` or as a dependency for another
project.




Structure
---------

Your program should be structured as follows:

 - `project/`: Source code, change `project` to reflect your project name
  - `project/extern/`: All external code, e.g. MATLAB and C  
    Example scripts for interacting with matlab and converting .mat to .npy  
    files back and forth are provided there.  
 - `doc/`: Project documentation
 - `tests/`: Unit tests
 - `setup.py`: Installation script




Dependencies
------------

Python dependencies should be managed in the `setup.py` file. They will
automatically be installed when running `python setup.py install`.

Other language dependencies should go in `src/extern/`.




NumPy to C
----------

This skeleton contains a module that combines the comfort of NumPy with the computational
power of native C compiled code.

All code that shall be compiled to C must go in a `.pyx` file, all plain python code goes
in a `.py` file.

Also, all `.pyx` files must be registered in the `extensions` in `setup.py`, around line 17.
Registering these files enables the library to be installed using pip or `python setup.py install`.

**Before committing, make sure that you have compiled `.pyx` files to `.c` files once.** This
enables users to compile your extension without having to use cython but merely their C compiler.



References
----------

 - [Sample Project][1] by the Python Package Authority

 [1]: https://github.com/pypa/sampleproject
