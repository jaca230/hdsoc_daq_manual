# Software Dependencies

## PIONEER Repository

Some installations are on the PIONEER repository, which requires access to pull from. See [how to get access](miscellaneous.md#getting-access-to-the-pioneer-repository).

---

## Development Tools

### Overview

These tools include compilers, libraries, and other utilities that facilitate software development and installation.

### Installation Guide
This guide should work for ALMA9. You can use `dnf` for ALMA9, but I prefer to work with `yum`

1 **Install yum package manager**

```
sudo dnf install yum
```

2 **Update the package index**:

```
sudo yum update
```

3 **Enable the EPEL repository**:

```
sudo yum install epel-release
```

4 **Install Development Tools and Dependencies**:

```
sudo yum groupinstall "Development Tools"
sudo yum install cmake gcc-c++ gcc screen subversion binutils libX11-devel libXpm-devel libXft-devel libXext-devel
```

5 **Install Python3**

```
sudo yum install python3-devel
```

6 **Install CMake from Source**  

If the installed CMake version is **not** `>=3.23`, (you can check with `cmake --version`) follow these steps to install CMake manually:

6.1. **Remove Old CMake (If Installed)**

```
sudo yum remove -y cmake
```

Verify removal:
```bash
cmake --version  # Should return "command not found"
```

6.2. **Install Required Dependencies**

```
sudo yum groupinstall -y "Development Tools"
sudo yum install -y gcc gcc-c++ make openssl-devel
```

6.3. **Download and Install the Latest CMake from Source**

1. **Download the latest version** (Check [Kitware's website](https://cmake.org/download/) for the latest version):
   ```
   wget https://github.com/Kitware/CMake/releases/download/v3.29.0/cmake-3.29.0.tar.gz
   ```

2. **Extract the archive**:
   ```
   tar -xvzf cmake-3.29.0.tar.gz
   cd cmake-3.29.0
   ```

3. **Build and install**:
   ```
   ./bootstrap
   make -j$(nproc)
   sudo make install
   ```

4. **Verify the New Installation**:
   ```
   cmake --version
   ```

---

## Python Packages

### Overview

Although this DAQ is written mostly in C++, it interfaces with with Nalu Scientific's "naludaq" package, which is a python module used for interfacing with the board. However, our use case requires C++. To avoid rewriting all of Nalu Scientific's methods in C++, pybind is used to wrap some C++ methods around existing naludaq python methods.


### Installation Guide

Install any needed packages with pip. Two that are needed are:

```
pip install pybind11 naludaq
```

---

## ROOT

### Overview

[ROOT](https://root.cern.ch/) is an open-source data analysis framework developed by CERN. It is widely used in high-energy physics for data processing, statistical analysis, visualization, and storage. It is needed for some features of Midas.

### Installation Guide
General installaiton guides are provided by ROOT at their [Installing ROOT](https://root.cern/install/) and [Building ROOT from source](https://root.cern/install/build_from_source/) pages.

#### Using `yum` Package Manager

1 **Enable the EPEL repository**:

```
sudo yum install epel-release
```

2 **Download and Install ROOT**:

```
sudo yum install root
```

#### Building from source

1 **Example building latest stable branch from source**

```
git clone --branch latest-stable --depth=1 https://github.com/root-project/root.git root_src
mkdir root_build root_install && cd root_build
cmake -DCMAKE_INSTALL_PREFIX=../root_install ../root_src # && check cmake configuration output for warnings or errors
cmake --build . -- install -j4 # if you have 4 cores available for compilation
source ../root_install/bin/thisroot.sh # or thisroot.{fish,csh}
```

**Note**: Adjust the ROOT version and the download URL as needed. Always check for the latest version on the [official ROOT website](https://root.cern.ch/). Furthermore, if you are not building from source you are installing precompiled binaries, which may not be up to date versions of ROOT. For specific versions, you may need to build root from source.

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

For a general Midas installation, you can follow this [Linux Quick Start Guide](https://daq00.triumf.ca/MidasWiki/index.php/Quickstart_Linux). For the g-2 modified DAQ, we use a custom version of midas, which can be cloned and installed as follows:

1 **Set experiment name environment variable**

```
export MIDAS_EXPT_NAME=DAQ
```
2 **Create exptab file**

```
mkdir online
cd online
touch exptab
echo "$MIDAS_EXPT_NAME $(pwd) system" >> exptab
export MIDAS_EXPTAB=$(pwd)/exptab	
```
3 **Install Midas**

```
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

```
export MIDASSYS=$(pwd)
export PATH=$PATH:$MIDASSYS/bin
```
**Note**: you can hardcode the environment variables `MIDASSYS` (and add to path), `MIDAS_EXPTAB`, and `MIDAS_EXPT_NAME` by adding the appropriate commands to your .bashrc file. This way, the environment variables are set with each new terminal session for that user.

5 **(Optional) it is recommended to also install the midas python package**:

```
pip install -e $MIDASSYS/python --user
```

---

## Nalu Board Controller

### Overview

The Nalu Board Controller library is a C++ library that uses pybind to wrap around some existing naludaq python methods. It allows the midas frontend to use C++ methods to configure nalu scientific's boards. You can read more in on the [github page for this library](https://github.com/jaca230/nalu_board_controller).

### Installation Guide

This should be automatically installed when installing the [HDSoC DAQ midas frontend](software.md#hdsoc_daq). If you want to manually install, see the [installation guide on the github's readme](https://github.com/jaca230/nalu_board_controller?tab=readme-ov-file#installation-1).

---

## Nalu Event Collector

### Overview

The Nalu Event Collector library is a C++ library that handles event collection from a nalu scientific board at high data rates. It has been internally tested to handle data rates as high as 300 MB/s. The HDSoCv1 board can send at most ~55 MB/s (due to an internal hardware limit), so this software handles virtually all uses cases. The library can automatically handle collecting UDP packets from a nalu scientific board, parsing them, and collecting them into events. The library holds a buffer of these events that midas can pull from to form its own events. You can read more in on the [github page for this library](https://github.com/jaca230/nalu_event_collector).

### Installation Guide

This should be automatically installed when installing the [HDSoC DAQ midas frontend](software.md#hdsoc_daq). If you want to manually install, see the [installation guide on the github's readme](https://github.com/jaca230/nalu_event_collector?tab=readme-ov-file#installation).

---

## reflect-cpp

### Overview

Reflect-cpp is a C++ library that achieves some level of reflection in C++. For our use case, we just use it to convert C++ structs to json and json to C++ structs. This removes a lot of boiler plate code that would otherwise go into the ODB management. You can read more in on the [github page for this library](https://github.com/getml/reflect-cpp).

### Installation Guide

This should be automatically installed when installing the [HDSoC DAQ midas frontend](software.md#hdsoc_daq). If you want to manually install, see [reflect-cpp's installation guide](https://rfl.getml.com/install/#option-2-compilation-using-cmake). I suggest compiling using cmake.

---