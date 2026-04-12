# Jetson Orin Nano Setup Guide

This document details the step-by-step process for configuring the NVIDIA Jetson Orin Nano edge AI device.

---

## 1. Flashing JetPack SDK

-   **Action:** Downloaded the latest JetPack SD Card Image from the NVIDIA developer website.
-   **Action:** Used Balena Etcher on the host PC to flash the image to a 128GB microSD card.

---

## 2. First Boot and Configuration

-   **Action:** Inserted the microSD card into the Jetson and connected peripherals (monitor, keyboard, mouse, power).
-   **Action:** Completed the initial Ubuntu setup wizard on the device, including creating a user, setting a password, and connecting to the local Wi-Fi network.

---

## 3. ROS 2 Humble Installation

-   **Action:** Followed the same procedure as the host PC to install `ros-humble-desktop` on the Jetson. This ensures version consistency across the distributed system.

---

## 4. SSH Server Configuration

**Why This Is Important:** In real-world robotics, edge devices like the Jetson are often run "headless" (without a dedicated monitor). Setting up SSH (Secure Shell) allows you to remotely access the Jetson's terminal from your host PC, which is essential for deployment, debugging, and management.

-   **Action:** Installed the OpenSSH server on the Jetson.
    ```bash
    sudo apt update
    sudo apt install openssh-server
    ```
-   **Verification:** From the **host PC's terminal**, connected to the Jetson using its IP address.
    ```bash
    # Replace <jetson_user> and <jetson_ip_address> with your actual values
    ssh <jetson_user>@<jetson_ip_address>
    ```
    **Verified Outcome:** Successfully logged into the Jetson's command line from the host PC without any connection errors.

---

## 5. Network Bridge Verification

This is the final test to confirm the entire distributed system is operational.

-   **Objective:** Verify that ROS 2 nodes on the host PC and Jetson can discover and communicate with each other over the local network.
-   **Procedure:**
    1.  Ran the `talker` demo node on the host PC (`192.168.68.75`).
    2.  Ran the `listener` demo node on the Jetson (`192.168.68.62`).
-   **Result:** **Success.** The Jetson's `listener` terminal successfully received the "Hello World" messages published from the host PC.
-   **Firewall Configuration Note:** A common issue preventing ROS 2 node discovery is a restrictive firewall. On both the host and the Jetson, the default `ufw` (Uncomplicated Firewall) is often inactive. However, if it has been enabled, you must ensure it allows the ports used by ROS 2's DDS middleware.
    -   **Verification Action:** Check the firewall status on both machines.
        ```bash
        sudo ufw status
        # Expected/Ideal Output for this project: Status: inactive
        ```
    -   If active, rules would be needed to allow traffic. For this learning environment, ensuring it remains inactive is the simplest approach.
-   **Additional Introspection Tools Verification:**
    -   `ros2 node list`: Correctly showed both `/talker` and `/listener` nodes on both machines.
    -   `ros2 topic info /chatter`: Correctly showed 1 publisher and 1 subscriber.
    -   `rqt_graph`: Correctly visualized the node graph showing the connection between the two nodes via the `/chatter` topic.

This successful test confirms that the distributed computing environment is fully configured and ready for development.