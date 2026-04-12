# Phase 1.5: Cloud Simulation Architecture (GCP Node)

## Overview
This document details the configuration of the cloud-based simulation node within the distributed robotics infrastructure. To achieve high-fidelity physics and sensor simulation (Sim-to-Real), this architecture leverages a GPU-accelerated virtual machine on Google Cloud Platform (GCP) running NVIDIA Isaac Sim. 

This node acts as the "Digital Twin" environment, streaming data to and receiving control inputs from the physical edge device (NVIDIA Jetson Orin Nano).

## 🏗️ System Architecture (Cloud-to-Edge)
* **The Model (Cloud):** GCP `n1-standard-8` (or similar) instance equipped with an NVIDIA T4 or L4 Tensor Core GPU. Runs the Isaac Sim Docker container and the ROS 2 simulation bridge.
* **The Interface (Network):** A Virtual Private Cloud (VPC) configured with strict firewall rules to allow Data Distribution Service (DDS) traffic for ROS 2, enabling seamless multi-machine discovery over a VPN (e.g., Tailscale or WireGuard).
* **The Hardware (Edge):** NVIDIA Jetson Orin Nano running the control logic and perception pipelines (documented in `jetson-setup.md`).

## 🛠️ Provisioning the Cloud Node
The following parameters define the minimum viable infrastructure for the simulation node:

### 1. GCP Compute Engine Configuration
* **Machine Type:** Minimum 8 vCPUs, 32GB RAM.
* **GPU:** 1x NVIDIA T4 (minimum) or L4 (recommended for complex raytracing).
* **OS Image:** Ubuntu 22.04 LTS.
* **Boot Disk:** 250GB SSD (Isaac Sim caches and Docker images require significant storage).

### 2. Infrastructure as Code (Conceptual)
To ensure system reproducibility, the setup process should be scripted:
1.  **Driver Installation:** Install NVIDIA Linux Grid drivers and the CUDA toolkit.
2.  **Containerization:** Install Docker Engine and the NVIDIA Container Toolkit.
3.  **Isaac Sim Deployment:** Pull and execute the `nvcr.io/nvidia/isaac-sim` container, exposing the necessary ports for the Omniverse WebRTC streaming client and ROS 2 bridges.

### 3. Network Discovery (The DDS Bridge)
For the Jetson Orin to control the cloud simulation, ROS 2 DDS traffic must flow across the network boundary.
* Implement a lightweight mesh VPN (Tailscale) to place the GCP node and the Jetson Orin on the same virtual subnet.
* Configure the `FASTRTPS_DEFAULT_PROFILES_FILE` to explicitly define the peer IPs, bypassing multicast restrictions common in cloud environments.

## ✅ Verification Protocol
To verify the system architecture is stable:
1.  Launch the Isaac Sim container on the GCP node.
2.  Connect to the Omniverse WebRTC interface via a local browser.
3.  From the physical Jetson terminal, execute `ros2 topic list`. The simulation topics (e.g., `/tf`, `/joint_states`) must be visible and actively publishing.
