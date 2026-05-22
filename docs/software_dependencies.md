# Software Dependencies

## PIONEER Repository

Some installations are on the PIONEER repository, which requires access to pull from. See [how to get access](miscellaneous.md#getting-access-to-the-pioneer-repository).

---

## Development Tools

### Overview

These tools include compilers, CMake, Python development support, and other utilities that facilitate software development and installation.

### Installation Guide

This guide should work for ALMA9. You can use `dnf` for ALMA9, but I prefer to work with `yum`.

1 **Install yum package manager**

```bash
sudo dnf install yum
```

2 **Update the package index**

```bash
sudo yum update
```

3 **Enable the EPEL repository**

```bash
sudo yum install epel-release
```

4 **Install Development Tools and Dependencies**

```bash
sudo yum groupinstall "Development Tools"
sudo yum install cmake gcc-c++ gcc screen subversion binutils libX11-devel libXpm-devel libXft-devel libXext-devel python3 python3-devel python3-pip
```

5 **Check the CMake version**

```bash
cmake --version
```

`hdsoc_daq` currently requires CMake `>= 3.23`.

If the installed CMake version is too old, follow these steps to install a newer version manually:

```bash
wget https://github.com/Kitware/CMake/releases/download/v3.29.0/cmake-3.29.0.tar.gz
tar -xvzf cmake-3.29.0.tar.gz
cd cmake-3.29.0
./bootstrap
make -j$(nproc)
sudo make install
```

Always check [Kitware's website](https://cmake.org/download/) for the current version before copying the version number above.

---

## Python Packages

### Overview

The DAQ still depends on a Python board-control stack even though the frontend itself is written mostly in C++. The current setup uses a repo-local virtual environment to hold the Python runtime needed by the board controller path.

### Installation Guide

The recommended way to set this up is with the repo helper:

```bash
./scripts/environment/helpers/setup_venv.sh
```

This creates or refreshes a virtual environment at:

```bash
.atar_daq_venv
```

and installs the requirements from:

```bash
requirements/board_tools.txt
```

At the moment, that requirements file includes:

```text
naludaq==0.36.0
naluconfigs==18.0.1
```

If you are not using the repo-local virtual environment, you will need those packages available in the Python environment used at runtime.

---

## ROOT

### Overview

[ROOT](https://root.cern.ch/) is an open-source data analysis framework developed by CERN. It is needed for some MIDAS features.

### Installation Guide

General installation guides are provided by ROOT at their [Installing ROOT](https://root.cern/install/) and [Building ROOT from source](https://root.cern/install/build_from_source/) pages.

#### Using `yum` Package Manager

1 **Enable the EPEL repository**

```bash
sudo yum install epel-release
```

2 **Download and Install ROOT**

```bash
sudo yum install root
```

#### Building from source

1 **Example building latest stable branch from source**

```bash
git clone --branch latest-stable --depth=1 https://github.com/root-project/root.git root_src
mkdir root_build root_install && cd root_build
cmake -DCMAKE_INSTALL_PREFIX=../root_install ../root_src
cmake --build . --target install -j4
source ../root_install/bin/thisroot.sh
```

**Note**: Adjust the ROOT version and the download URL as needed. Always check for the latest version on the [official ROOT website](https://root.cern.ch/).

---

## Midas

### Overview

[Midas](https://daq00.triumf.ca/MidasWiki/index.php/Main_Page) is a data acquisition system used in high-energy physics experiments.
Midas provides the following functionalities:

- Run control
- Experiment configuration
- Data readout
- Event building
- Data storage
- Slow control
- Alarm systems
- ... much more ...

### Installation Guide

For a general MIDAS installation, you can follow this [Linux Quick Start Guide](https://daq00.triumf.ca/MidasWiki/index.php/Quickstart_Linux).

`hdsoc_daq` expects `MIDASSYS` to point to a working MIDAS install before configuration. In particular, the build checks for:

- `$MIDASSYS/include`
- `$MIDASSYS/lib/libmidas.a`
- `$MIDASSYS/lib/libmfe.a`

For the g-2 modified DAQ, we use a custom version of MIDAS, which can be cloned and installed as follows:

1 **Set experiment name environment variable**

```bash
export MIDAS_EXPT_NAME=ATAR_DAQ
```

2 **Create exptab file**

```bash
mkdir online
cd online
touch exptab
echo "$MIDAS_EXPT_NAME $(pwd) system" >> exptab
export MIDAS_EXPTAB=$(pwd)/exptab
```

3 **Install MIDAS**

```bash
cd ..
mkdir packages
git clone --recursive git@github.com:PIONEER-Experiment/midas-modified.git midas
cd midas
mkdir build
cd build
cmake ..
make -j$(nproc) install
cd ..
```

4 **Set `MIDASSYS` environment variable and add to path**

```bash
export MIDASSYS=$(pwd)
export PATH=$PATH:$MIDASSYS/bin
```

**Note**: You can hardcode the environment variables `MIDASSYS`, `MIDAS_EXPTAB`, and `MIDAS_EXPT_NAME` by adding the appropriate commands to your `.bashrc` file. The repo also provides environment helpers documented on the [scripts page](scripts.md#environment-setup).

5 **(Optional) it is recommended to also install the MIDAS Python package**

```bash
pip install -e $MIDASSYS/python --user
```

---

## CPM Managed Libraries

### Overview

Several dependencies used by `hdsoc_daq` are no longer meant to be installed manually as part of the normal setup flow. They are fetched automatically by CPM during the CMake configure step.

These include:

- `nalu_event_collector`
- `nalu_board_controller`
- `reflect-cpp`
- `spdlog`
- `nlohmann/json`
- `pybind11`

### Installation Guide

No separate manual installation step is needed for the normal `hdsoc_daq` build. Once `MIDASSYS` is set and the Python environment is available, running:

```bash
./scripts/build.sh
```

will configure CMake and let CPM pull the required C++ packages automatically.

If you want to inspect or build these projects separately, see their upstream repositories:

- [nalu_board_controller](https://github.com/jaca230/nalu_board_controller)
- [nalu_event_collector](https://github.com/jaca230/nalu_event_collector)
- [reflect-cpp](https://github.com/getml/reflect-cpp)

---
