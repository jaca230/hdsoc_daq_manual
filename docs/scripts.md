# Scripts

## Top Level

### build.sh

| **Field**        | **Description**                                                  |
|------------------|------------------------------------------------------------------|
| **Path**         | `$ATAR_DAQ_DIR/scripts/build.sh` |
| **Description**  | Builds the project using CMake. It loads the repository environment first, then configures and builds the project. |
| **Flags**        | `-o, --overwrite` → Remove the existing build directory before building. <br> `--venv PATH` → Override the repo-local virtual environment path. <br> `--system-python` → Ignore the repo-local virtual environment and use the system Python setup. |
| **Example Usage**| `./scripts/build.sh` <br> `./scripts/build.sh --overwrite` |

### run.sh

| **Field**        | **Description**                                                  |
|------------------|------------------------------------------------------------------|
| **Path**         | `$ATAR_DAQ_DIR/scripts/run.sh` |
| **Description**  | Runs the `frontend` executable. It can build first, set up the repo-local virtual environment, and run under `gdb`. |
| **Flags**        | `--build` → Build before running. <br> `--overwrite` → Rebuild from a clean build directory when used with `--build`. <br> `--setup-venv` → Create or update the repo-local Python environment before running. <br> `--venv PATH` → Override the repo-local virtual environment path. <br> `--system-python` → Skip the repo-local virtual environment and use the system Python setup. <br> `--debug` → Run the executable in GDB. <br> `-i <number>` → Specifies an index (default: `0`). |
| **Example Usage**| `./scripts/run.sh -i 0` <br> `./scripts/run.sh --build -i 0` <br> `./scripts/run.sh --setup-venv -i 0` |

---

## Data management

### delete_data.sh

| **Field**        | **Description**                                                  |
|------------------|------------------------------------------------------------------|
| **Path**         | `$ATAR_DAQ_DIR/scripts/data_management/delete_data.sh` |
| **Description**  | Deletes MIDAS data files in the experiment directory. If `--dry-run` is used, it lists files without deleting them. |
| **Flags**        | `--dry-run` → Lists files that would be deleted without removing them. |
| **Example Usage**| `./scripts/data_management/delete_data.sh` <br> `./scripts/data_management/delete_data.sh --dry-run` |

### find_data_dir.sh

| **Field**        | **Description**                                                  |
|------------------|------------------------------------------------------------------|
| **Path**         | `$ATAR_DAQ_DIR/scripts/data_management/find_data_dir.sh` |
| **Description**  | Finds the experiment data directory from `MIDAS_EXPTAB` and `MIDAS_EXPT_NAME`, then writes it to `experiment_dir.txt`. |
| **Flags**        | _(None)_ |
| **Example Usage**| `./scripts/data_management/find_data_dir.sh` |

---

## Environment Setup

### Overview

The old `scripts/environment_setup` helpers have been replaced by a newer environment system under:

```text
scripts/environment/
scripts/environment/helpers/
```

The main user entrypoint is:

```bash
source ./scripts/environment/activate_environment.sh
```

This helper will detect and load MIDAS environment variables, optionally create the repo-local Python virtual environment, and activate it.

### activate_environment.sh

| **Field**        | **Description**                                                  |
|------------------|------------------------------------------------------------------|
| **Path**         | `$ATAR_DAQ_DIR/scripts/environment/activate_environment.sh` |
| **Description**  | Main shell entrypoint for preparing the ATAR DAQ environment. It detects and saves MIDAS-related environment variables if needed, creates or refreshes the repo-local virtual environment if needed, and activates it. |
| **Flags**        | `--quiet` → Suppress informational output. <br> `--no-midas-bin` → Do not prepend `MIDASSYS/bin` to `PATH`. <br> `--system-python` → Skip the repo-local virtual environment and use the system Python setup. <br> `--venv PATH` → Override the virtual environment path. |
| **Example Usage**| `source ./scripts/environment/activate_environment.sh` |

### detect_midas_environment.sh

| **Field**        | **Description**                                                  |
|------------------|------------------------------------------------------------------|
| **Path**         | `$ATAR_DAQ_DIR/scripts/environment/helpers/detect_midas_environment.sh` |
| **Description**  | Searches for the `midas` directory and `exptab` file, sets `MIDASSYS`, `MIDAS_EXPTAB`, and `MIDAS_EXPT_NAME`, and saves them to `scripts/environment/helpers/environment_variables.sh`. |
| **Flags**        | `--output PATH` → Override the output file path. <br> `-q, --quiet` → Suppress the summary output. |
| **Example Usage**| `./scripts/environment/helpers/detect_midas_environment.sh` |

### load_environment.sh

| **Field**        | **Description**                                                  |
|------------------|------------------------------------------------------------------|
| **Path**         | `$ATAR_DAQ_DIR/scripts/environment/helpers/load_environment.sh` |
| **Description**  | Loads the saved repository environment variables and optionally configures access to the repo-local virtual environment. This helper is used internally by `build.sh`, `run.sh`, and other scripts. |
| **Flags**        | `--quiet` → Suppress informational output. <br> `--add-midas-bin` → Prepend `MIDASSYS/bin` to `PATH`. <br> `--no-venv` → Do not activate or expose the repo-local virtual environment. <br> `--setup-venv` → Create or update the repo-local virtual environment before loading it. <br> `--system-python` → Ignore the repo-local virtual environment and isolate from user-site Python. <br> `--venv PATH` → Override the virtual environment path. |
| **Example Usage**| `source ./scripts/environment/helpers/load_environment.sh --add-midas-bin` |

### setup_venv.sh

| **Field**        | **Description**                                                  |
|------------------|------------------------------------------------------------------|
| **Path**         | `$ATAR_DAQ_DIR/scripts/environment/helpers/setup_venv.sh` |
| **Description**  | Creates or updates the repo-local Python environment used by board-controller-backed tools. It installs the requirements from `requirements/board_tools.txt`. |
| **Flags**        | `--venv PATH` → Override the virtual environment path. <br> `--python BIN` → Python executable to use for venv creation. <br> `--requirements PATH` → Requirements file to install. <br> `--recreate` → Delete and recreate the virtual environment. |
| **Example Usage**| `./scripts/environment/helpers/setup_venv.sh` <br> `./scripts/environment/helpers/setup_venv.sh --recreate` |

### activate_venv.sh

| **Field**        | **Description**                                                  |
|------------------|------------------------------------------------------------------|
| **Path**         | `$ATAR_DAQ_DIR/scripts/environment/helpers/activate_venv.sh` |
| **Description**  | Activates only the repo-local virtual environment. |
| **Flags**        | _(None)_ |
| **Example Usage**| `source ./scripts/environment/helpers/activate_venv.sh` |

### clear_environment.sh

| **Field**        | **Description**                                                  |
|------------------|------------------------------------------------------------------|
| **Path**         | `$ATAR_DAQ_DIR/scripts/environment/helpers/clear_environment.sh` |
| **Description**  | Clears the MIDAS, ATAR DAQ, and Python environment variables set by the environment helpers. |
| **Flags**        | _(None)_ |
| **Example Usage**| `source ./scripts/environment/helpers/clear_environment.sh` |

---

## ODB

### set_enabled_channels.py

| Field            | Description                                                     |
|------------------|-----------------------------------------------------------------|
| Path             | `$ATAR_DAQ_DIR/scripts/odb/set_enabled_channels.py` |
| Description      | Updates the enabled channels in the ODB by setting the number of enabled channels from the start (`0`) and disabling the rest. |
| Flags            | `num_enabled_channels` → The number of enabled channels, between `0` and `32`. |
| Example Usage    | `./scripts/odb/set_enabled_channels.py 16` <br> Enables the first 16 channels and disables the rest. |

## Screen Control

### screen_frontend.sh

| Field              | Description                                                     |
|--------------------|-----------------------------------------------------------------|
| Path               | `$ATAR_DAQ_DIR/scripts/screen_control/screen_frontend.sh` |
| Description        | Starts the frontend inside a detached `screen` session. |
| Flags              | `-i` → Index for the session name (defaults to `0`). <br> `--setup-venv` → Create or update the repo-local virtual environment before running. <br> `--venv PATH` → Override the virtual environment path. <br> `--system-python` → Skip the repo-local virtual environment and use the system Python setup. |
| Example Usage      | `./scripts/screen_control/screen_frontend.sh -i 1` |

### stop_screen.sh

| Field              | Description                                                     |
|--------------------|-----------------------------------------------------------------|
| Path               | `$ATAR_DAQ_DIR/scripts/screen_control/stop_screen.sh` |
| Description        | Stops a running `screen` session specified by the index. |
| Flags              | `-i` → Index for the session name (defaults to `0`). |
| Example Usage      | `./scripts/screen_control/stop_screen.sh -i 1` |

---

## Webpage Scripts

### start_midas_webpage.sh

| Field              | Description                                                     |
|--------------------|-----------------------------------------------------------------|
| Path               | `$ATAR_DAQ_DIR/scripts/webpage_scripts/start_midas_webpage.sh` |
| Description        | Starts processes in the background, each inside a `screen` session, using process names from a `screen_names.txt` file. |
| Flags              | None. |
| Example Usage      | `./scripts/webpage_scripts/start_midas_webpage.sh` |

### stop_midas_webpage.sh

| Field              | Description                                                     |
|--------------------|-----------------------------------------------------------------|
| Path               | `$ATAR_DAQ_DIR/scripts/webpage_scripts/stop_midas_webpage.sh` |
| Description        | Stops processes running in `screen` sessions based on names listed in `screen_names.txt`. |
| Flags              | None. |
| Example Usage      | `./scripts/webpage_scripts/stop_midas_webpage.sh` |

---
