# Host PC Setup Guide

This document details the step-by-step process for configuring the host development workstation.

---

## 1. OS Installation: Dual-Boot Ubuntu 22.04 LTS

-   **Action:** Created a 100GB+ partition on the main SSD from within Windows.
-   **Action:** Disabled Fast Startup in Windows and Secure Boot in the system's UEFI/BIOS.
-   **Action:** Installed Ubuntu 22.04 LTS from a bootable USB drive onto the newly created partition.
-   **Verification:** Confirmed successful boot into the Ubuntu desktop and verified the correct version was installed.
    ```bash
    lsb_release -a
    # Verified Output: Ubuntu 22.04.x LTS
    ```

---

## 2. NVIDIA Driver Installation

-   **Action:** Updated all system packages using `sudo apt update && sudo apt upgrade`.
-   **Action:** Identified the recommended proprietary driver for my hardware using `ubuntu-drivers devices`.
-   **Action:** Installed the driver using `sudo ubuntu-drivers autoinstall`. Handled MOK enrollment for Secure Boot during the reboot process.
-   **Verification:** Confirmed successful driver installation and communication with the GPU. The `nvidia-smi` command runs without errors and correctly identifies the hardware.

    **Verified Output:**
    ```
    +-----------------------------------------------------------------------------------------+
    | NVIDIA-SMI 575.64.03        Driver Version: 575.64.03    CUDA Version: 12.9     |
    |-----------------------------------------+------------------------+----------------------+
    | GPU  Name                  Persistence-M| Bus-Id          Disp.A#| Volatile Uncorr. ECC |
    | Fan  Temp   Perf          Pwr:Usage/Cap|           Memory-Usage | GPU-Util  Compute M. |
    |=========================================+========================+======================|
    |   0  NVIDIA GeForce RTX 2070 ...   Off  |   00000000:01:00.0  On |                  N/A |
    | N/A   44C    P8              6W /   80W|       87MiB /  8192MiB |      8%      Default |
    +-----------------------------------------+------------------------+----------------------+
    ```

---

## 3. ROS 2 Humble Installation

-   **Action:** Followed the official ROS 2 documentation to add the required repositories and install the `ros-humble-desktop` package.
-   **Action:** Added the `source /opt/ros/humble/setup.bash` command to the `.bashrc` file for convenience.
-   **Verification:** Opened a new terminal and confirmed that the ROS 2 environment variables were set.
    ```bash
    printenv ROS_DISTRO
    # Verified Output: humble
    ```

---

## 4. NVIDIA Isaac Sim Installation

**Why This Is Important:** Isaac Sim is the core simulation platform for this entire learning track. Verifying its installation is a critical prerequisite for Phase 2, where we will begin scripting and controlling robots within the simulator.

-   **Action:** Downloaded and installed the **NVIDIA Omniverse Launcher**.
-   **Action:** From the Launcher's "Exchange" tab, downloaded and installed **Isaac Sim** (Version 2023.1.1 or later recommended).
-   **Action:** After installation, navigated to the Isaac Sim installation directory (e.g., `~/.local/share/ov/pkg/isaac-sim-2023.1.1`) and ran the initial setup script.
    ```bash
    ./setup_conda.sh
    ```
-   **Verification:** Launched Isaac Sim to confirm a successful installation. The main GUI should load without errors.
    ```bash
    ./isaac-sim.sh
    ```
    **Verified Outcome:** The NVIDIA Isaac Sim application window opens, showing the main viewport and UI elements. This confirms that the simulator and all its bundled Python dependencies are correctly installed.

---

## 5. Core Development Tools Installation

**Why This Is Important:** While the `ros-humble-desktop` package installs many dependencies, explicitly installing `git` and `colcon` ensures the tools required for version control and building ROS 2 workspaces are present and verified.

-   **Action:** Installed Git for version control and `colcon`, the standard build tool for ROS 2 workspaces.
    ```bash
    sudo apt update
    sudo apt install git python3-colcon-common-extensions
    ```
-   **Verification:** Checked the version of each tool to confirm successful installation.
    ```bash
    git --version
    # Expected Output: git version 2.34.1 or similar

    colcon --version
    # Expected Output: colcon version 0.14.2 or similar
    ```