# Scripts

## Top Level

### build.sh

| **Field**        | **Description**                                                  |
|------------------|------------------------------------------------------------------|
| **Path**         | `$ATAR_DAQ_DIR/scripts/build.sh`                                              |
| **Description**  | Builds the project using CMake and Make. If the `--overwrite` flag is used, it cleans the previous build first. |
| **Flags**        | `-o, --overwrite` → Remove the existing build directory before building. |
| **Example Usage**| `./build.sh` <br> `./build.sh --overwrite` |

### run.sh

| **Field**        | **Description**                                                  |
|------------------|------------------------------------------------------------------|
| **Path**         | `$ATAR_DAQ_DIR/scripts/run.sh`                                                |
| **Description**  | Runs the `frontend` executable. Supports running in background mode, with debugging, and setting an index. |
| **Flags**        | `--debug` → Runs the executable in GDB. <br> <br> `-i <number>` → Specifies an index (default: 0). <br> `--help` → Displays usage help. |
| **Example Usage**| `./run.sh` <br> `./run.sh --debug` <br> `./run.sh -i 2` |

---

## Data management

### delete_data.sh

| **Field**        | **Description**                                                  |
|------------------|------------------------------------------------------------------|
| **Path**         | `$ATAR_DAQ_DIR/scripts/delete_data.sh` |
| **Description**  | Deletes MIDAS data files in the experiment directory. If `--dry-run` is used, it lists files without deleting them. |
| **Flags**        | `--dry-run` → Lists files that would be deleted without removing them. |
| **Example Usage**| `./delete_data.sh` <br> `./delete_data.sh --dry-run` |


### find_data_dir.sh

| **Field**        | **Description**                                                  |
|------------------|------------------------------------------------------------------|
| **Path**         | `$ATAR_DAQ_DIR/scripts/find_data_dir.sh` |
| **Description**  | Finds the experiment data directory and writes it to `experiment_dir.txt`. |
| **Flags**        | _(None)_ |
| **Example Usage**| `./find_data_dir.sh` |

---

## Environment Setup

### clear_environment.sh  

| **Field**        | **Description**                                                  |
|------------------|------------------------------------------------------------------|
| **Path**         | `$ATAR_DAQ_DIR/scripts/environment_setup/clear_environment.sh` |
| **Description**  | Clears the MIDAS environment variables by unsetting `MIDASSYS`, `MIDAS_EXPTAB`, and `MIDAS_EXPT_NAME`. |
| **Flags**        | _(None)_ |
| **Example Usage**| `./clear_environment.sh` |


### detect_environment.sh  

| **Field**        | **Description**                                                  |
|------------------|------------------------------------------------------------------|
| **Path**         | `$ATAR_DAQ_DIR/scripts/environment_setup/detect_environment.sh` |
| **Description**  | Searches for the `midas` directory and `exptab` file, sets `MIDASSYS`, `MIDAS_EXPTAB`, and `MIDAS_EXPT_NAME`, and saves them to `environment_variables.txt`. |
| **Flags**        | _(None)_ |
| **Example Usage**| `./detect_environment.sh` |


### setup_environment.sh  

| **Field**        | **Description**                                                  |
|------------------|------------------------------------------------------------------|
| **Path**         | `$ATAR_DAQ_DIR/scripts/environment_setup/setup_environment.sh` |
| **Description**  | Reads `environment_variables.txt` to set environment variables and optionally adds `MIDASSYS/bin` to the `PATH`. |
| **Flags**        | `-a, --add` → Adds `MIDASSYS/bin` to `PATH` if `MIDASSYS` is set. <br> `-q, --quiet` → Suppresses all output. <br> `-h, --help` → Displays usage help. |
| **Example Usage**| `./setup_environment.sh` <br> `./setup_environment.sh --add` <br> `./setup_environment.sh --quiet` |

---

## Install Libraries

### install_dependencies.sh

| Field            | Description                                                     |
|------------------|-----------------------------------------------------------------|
| Path             | `$ATAR_DAQ_DIR/scripts/install_libaries/install_dependencies.sh` |
| Description      | Installs all required dependencies by calling their respective installation scripts. |
| Flags            | (None)                                                         |
| Example Usage    | `./install_dependencies.sh`                                     |

### install_reflect_cpp.sh

| Field            | Description                                                     |
|------------------|-----------------------------------------------------------------|
| Path             | `$ATAR_DAQ_DIR/scripts/install_libaries/install_reflect_cpp.sh` |
| Description      | Installs the Reflect-C++ library, allowing customization of installation directory, C++ standard, and build type. |
| Flags            | `-o, --overwrite` → Removes the previous build before installing. <br> `-p, --prefix <path>` → Specifies the installation directory (default: /usr/local). <br> `-s, --cxx-standard <version>` → Sets the C++ standard (default: 20). <br> `-b, --build-type <type>` → Sets the build type (default: Release). |
| Example Usage    | `./install_reflect_cpp.sh` <br> `./install_reflect_cpp.sh --overwrite` <br> `./install_reflect_cpp.sh --prefix /opt/custom` <br> `./install_reflect_cpp.sh --cxx-standard 17 --build-type Debug` |

---

## ODB

### set_enabled_channels.py

| Field            | Description                                                     |
|------------------|-----------------------------------------------------------------|
| Path             | `$ATAR_DAQ_DIR/scripts/odb/set_enabled_channels.py`             |
| Description      | Updates the enabled channels in the ODB by setting the number of enabled channels from the start (0) and disabling the rest. |
| Flags            | `num_enabled_channels` → The number of enabled channels (between 0 and 32). |
| Example Usage    | `./set_enabled_channels.py 16` <br> Enables the first 16 channels and disables the rest. |

## Screen Control

### screen_frontend.sh

| Field              | Description                                                     |
|--------------------|-----------------------------------------------------------------|
| Path               | `$ATAR_DAQ_DIR/scripts/screen_control/screen_frontend.sh`       |
| Description        | Starts a specified script inside a `screen` session, optionally passing an index value. |
| Flags              | `-i` → Index for the session name (defaults to 0).             |
| Example Usage      | `./screen_frontend.sh -i 1` <br> Starts the script `run.sh` inside a `screen` session with index 1. |


### stop_screen.sh

| Field              | Description                                                     |
|--------------------|-----------------------------------------------------------------|
| Path               | `$ATAR_DAQ_DIR/scripts/screen_control/stop_screen.sh`          |
| Description        | Stops a running `screen` session specified by the index.       |
| Flags              | `-i` → Index for the session name (defaults to 0).             |
| Example Usage      | `./stop_screen.sh -i 1` <br> Stops the `screen` session with index 1. |

---

## Webpage Scripts

### start_midas_webpage.sh

| Field              | Description                                                     |
|--------------------|-----------------------------------------------------------------|
| Path               | `$ATAR_DAQ_DIR/scripts/webpage_scripts/start_midas_webpage.sh` |
| Description        | Starts processes in the background, each inside a `screen` session, using process names from a `screen_names.txt` file. |
| Flags              | None.                                                           |
| Example Usage      | `./start_midas_webpage.sh` <br> Starts all processes defined in `screen_names.txt`. |


### stop_midas_webpage.sh

| Field              | Description                                                     |
|--------------------|-----------------------------------------------------------------|
| Path               | `$ATAR_DAQ_DIR/scripts/webpage_scripts/stop_midas_webpage.sh`  |
| Description        | Stops processes running in `screen` sessions based on names listed in `screen_names.txt`. |
| Flags              | None.                                                           |
| Example Usage      | `./stop_midas_webpage.sh` <br> Stops all processes defined in `screen_names.txt`. |

---


