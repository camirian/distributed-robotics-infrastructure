# Phase 1: AI Robotics Professional Development Environment

This repository documents the complete setup and configuration of a professional-grade development environment for advanced robotics and AI applications. The goal is to establish a robust, reproducible, and distributed system consisting of a powerful host development workstation and a physical edge AI device (NVIDIA Jetson).

This setup serves as the foundational environment for all subsequent projects in my AI Robotics Portfolio. For definitions of key terms, please see my central **[AI & Robotics Glossary](https://github.com/camirian/phase-0-robotics-glossary/blob/main/GLOSSARY.md)**.

---

## ✅ Skills Demonstrated

Successfully completing this foundational setup demonstrates core competencies in:

-   **Systems Administration:** Proficiently installing and configuring a Linux (Ubuntu 22.04) environment from scratch, including disk partitioning for dual-boot systems.
-   **Hardware & Driver Management:** Correctly installing and verifying proprietary NVIDIA drivers on Linux, including handling dependencies and Secure Boot (MOK) enrollment.
-   **Distributed Systems & Networking:** Establishing and verifying a multi-machine ROS 2 network, proving an understanding of the DDS discovery mechanism.
-   **Embedded & Edge AI Systems:** Flashing and configuring an embedded device (NVIDIA Jetson) with the JetPack SDK, preparing it for sim-to-real deployment.
-   **Version Control & Professional Documentation:** Utilizing Git and GitHub for version control and maintaining high-quality, structured documentation for a technical project.

---

## 🛠️ Software Stack & Key Tools

| Component             | Version / Type                   | Purpose                                    |
| --------------------- | -------------------------------- | ------------------------------------------ |
| Operating System      | Ubuntu 22.04 LTS                 | Standard for robotics development          |
| Robotics Middleware   | [ROS 2 Humble](https://github.com/camirian/phase-0-robotics-glossary/blob/main/GLOSSARY.md#ros-ros-2) | Core communication and tooling framework   |
| GPU Driver            | NVIDIA Proprietary Driver 5xx.xx | Enables GPU acceleration for AI/Sim        |
| Simulation Platform   | [Isaac Sim](https://github.com/camirian/phase-0-robotics-glossary/blob/main/GLOSSARY.md#isaac-sim) | High-fidelity physics simulation & sensor data |
| Edge AI SDK           | [JetPack SDK](https://github.com/camirian/phase-0-robotics-glossary/blob/main/GLOSSARY.md#jetpack-sdk) | OS & libraries for the Jetson platform     |
| Version Control       | [Git](https://github.com/camirian/phase-0-robotics-glossary/blob/main/GLOSSARY.md#git) | Tracking changes and managing project history |
| Code Hosting          | [GitHub](https://github.com/camirian/phase-0-robotics-glossary/blob/main/GLOSSARY.md#github) / `gh` CLI | Publicly showcasing and managing repositories |
| Build Tool            | [Colcon](https://github.com/camirian/phase-0-robotics-glossary/blob/main/GLOSSARY.md#colcon) | Building ROS 2 packages and workspaces     |

---

## 📝 Setup & Verification Details

Detailed, step-by-step instructions and verification checklists for each component are located in the following documents:

-   [`host-pc-setup.md`](./host-pc-setup.md): Complete guide for the host workstation setup.
-   [`jetson-setup.md`](./jetson-setup.md): Complete guide for the Jetson Orin Nano setup.

---

## 📜 License

This project is licensed under the Apache 2.0 License. See the [`LICENSE`](./LICENSE) file for details.