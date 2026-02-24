# Engineering Build Log: Distributed AI Robotics Infrastructure

## 1. The Core Objective (The "Why")
To build a deterministic, low-latency bridge between a high-compute simulation host (Ubuntu 22.04), a cloud-based GPU simulation node (GCP), and a physical edge compute node (NVIDIA Jetson Orin Nano). This project closes the gap between cloud-level AI inference and physical hardware actuation, establishing the foundational network topology required for scalable, L5 autonomous robotic swarms.

## 2. The Toolchain & Constraints
* **OS & Middleware:** Ubuntu 22.04 LTS, ROS 2 (Humble Hawksbill)
* **Hardware:** High-Compute Host PC + NVIDIA Jetson Orin Nano (Edge Node) + GCP Cloud Node
* **Network Protocol:** Data Distribution Service (DDS)
* **Underlying Engine:** NVIDIA Isaac Sim for high-fidelity physics and sensor data generation
* **The Hard Constraint:** Ensuring zero packet loss, GPU-accelerated rendering, and deterministic latency across the distributed ROS 2 network, regardless of the physical environment's Wi-Fi or Ethernet degradation.

## 3. The Execution Sequence
* **Step 1: Base Environment Provisioning:** Configured the Ubuntu Host, GCP Cloud Node, and Jetson edge node with identical ROS 2 Humble environments to prevent version-mismatch drift. Managed NVIDIA proprietary drivers (5xx) and JetPack SDK installation.
* **Step 2: Network Topography Setup:** Established the `ROS_DOMAIN_ID` and explicitly configured the DDS profiles (e.g., FastDDS/CycloneDDS) to allow cross-device node discovery across the host, edge, and cloud boundaries.
* **Step 3: Edge-to-Host Verification:** Deployed a lightweight telemetry publisher on the Jetson and a subscriber on the Host PC to verify bidirectional communication bandwidth and latency.
* **Step 4: System De-bottlenecking:** Tuned Linux kernel parameters (e.g., `sysctl` net core buffers) to optimize for high-frequency robotic telemetry.

## 4. Architectural Decisions & Trade-offs
* **Why explicit DDS tuning?** Default ROS 2 DDS configurations frequently drop high-frequency UDP packets over Wi-Fi. By tuning the DDS XML profiles, we ensure the infrastructure is reliable enough for mission-critical physical hardware, not just lab environments.
* **Why use a GCP Cloud Node alongside a Local Host?** While local hosts handle low-latency control, cloud nodes allow scalable batch processing and reinforcement learning execution in Isaac Sim without being strictly bound to physical workstation workstation limits.

## 5. The Wavefront (Next Steps)
* **Project Alpha:** Containerize the entire edge deployment using Docker and NVIDIA Container Runtime so the infrastructure can be flashed to a new Jetson node in under 5 minutes.
* **Project Beta:** Integrate real-time zero-trust network security (VPN/Tailscale) to allow the Host PC to securely command the Jetson node over a public WAN.
