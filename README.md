# Python binding for Fast DDS

<a href="http://www.eprosima.com"><img src="https://encrypted-tbn3.gstatic.com/images?q=tbn:ANd9GcSd0PDlVz1U_7MgdTe0FRIWD0Jc9_YH-gGi0ZpLkr-qgCI6ZEoJZ5GBqQ" align="left" hspace="8" vspace="2" width="100" height="100" ></a>

[![License](https://img.shields.io/github/license/eProsima/Fast-DDS-python.svg)](https://opensource.org/licenses/Apache-2.0)
[![Releases](https://img.shields.io/github/v/release/eProsima/Fast-DDS-python?sort=semver)](https://github.com/eProsima/Fast-DDS-python/releases)
[![Issues](https://img.shields.io/github/issues/eProsima/Fast-DDS-python.svg)](https://github.com/eProsima/Fast-DDS-python/issues)
[![Forks](https://img.shields.io/github/forks/eProsima/Fast-DDS-python.svg)](https://github.com/eProsima/Fast-DDS-python/network/members)
[![Stars](https://img.shields.io/github/stars/eProsima/Fast-DDS-python.svg)](https://github.com/eProsima/Fast-DDS-python/stargazers)
[![Fast DDS Python Ubuntu CI (nightly)](https://github.com/eProsima/Fast-DDS-Python/actions/workflows/nightly-ubuntu-ci.yml/badge.svg)](https://github.com/eProsima/Fast-DDS-Python/actions/workflows/nightly-ubuntu-ci.yml)
[![Fast DDS Python Windows CI (nightly)](https://github.com/eProsima/Fast-DDS-Python/actions/workflows/nightly-windows-ci.yml/badge.svg)](https://github.com/eProsima/Fast-DDS-Python/actions/workflows/nightly-windows-ci.yml)


*eProsima Fast DDS Python* is a Python binding for the [*eProsima Fast DDS*](https://github.com/eProsima/Fast-DDS) C++ library.
This is a work in progress, but ultimately the goal is having the complete *Fast DDS* API available in Python.
Two packages are available in this repository: the proper Python binding, `fastdds_python`, and the examples, `fastdds_python_examples`.

## Installation guide

This tutorial shows how to build *Fast DDS Python* using [colcon](https://colcon.readthedocs.io), a command line tool to build sets of software packages.
To do so, `colcon` and `vcstool` need to be installed:

```bash
pip install -U colcon-common-extensions vcstool
```

### Dependencies

*Fast DDS Python* depends on [Fast DDS](https://github.com/eProsima/Fast-DDS) and [Fast CDR](https://github.com/eProsima/Fast-CDR).
For simplicity, this tutorial will build these dependencies alongside the binding itself.
More advanced users can build or link to this packages separately.

Install *Fast DDS* dependencies running:

```bash
sudo apt update
sudo apt install -y \
    libasio-dev \
    libtinyxml2-dev
```

Additionally, *Fast DDS Python* also depends on [SWIG 4.0](http://www.swig.org/) and python3-dev. Install these dependencies running:
```bash
sudo apt update
sudo apt install -y \
    swig \
    libpython3-dev
```

### Build and install

```bash
# Create a `Fast-DDS-python` directory in which to download and build Fast DDS Python bindings and its dependencies:
mkdir ~/Fast-DDS-python
cd ~/Fast-DDS-python
# Get workspace setup file (note this address was changed to our fork and to v1.4.3, which is needed for compatibility with the controller messages).
wget https://raw.githubusercontent.com/foundationbot/Fast-DDS-python/v1.4.3/fastdds_python.repos
# Download repositories
mkdir src
vcs import src < fastdds_python.repos
# Build the workspace
colcon build
```

When running an instance of an application using Fast DDS Python bindings, the colcon overlay built in the dedicated Fast-DDS-python directory must be sourced. There are two possibilities:

Every time a new shell is opened, prepare the environment locally by typing the command:

```source ~/Fast-DDS-python/install/setup.bash```

Add the sourcing of the colcon overlay permanently to the PATH, by typing the following:

```echo 'source ~/Fast-DDS-python/install/setup.bash' >> ~/.bashrc```

Please, refer to [colcon documentation](https://colcon.readthedocs.io/en/released/reference/verb/build.html) for more information, such as building only one of the packages.

## Installing Fast-DDS Gen

### Java JDK
The JDK is a development environment for building applications and components using the Java language. There are several versions of Java available. For instance, to install Java 17 JDK, run the following command:

```sudo apt install openjdk-17-jdk```

Note: Fast DDS-Gen supports Java versions from 11 to 19.

### Compiling Fast-DDS Gen
In order to compile Fast DDS-Gen, an executable script is included in the repository which will download Gradle temporarily for the compilation step. Please, follow the steps below to build Fast DDS-Gen:

Note

Since Fast DDS was installed following the Colcon installation, Fast DDS-Gen’s repository can be found under the src directory within the colcon workspace.
```
cd ~/Fast-DDS/src
cd fastddsgen
./gradlew assemble
```
Note: In case that a supported Gradle version is already installed in the system, Fast DDS-Gen can also be built running directly:
```
gradle assemble
```

## Using Fast-DDS Gen to Generate Python Message

TODO

## Python example

Fast DDS documentation includes a first publisher-subscriber application using Python.
Please refer to [this section](https://fast-dds.docs.eprosima.com/en/latest/fastdds/getting_started/simple_python_app/simple_python_app.html#) for more information.
