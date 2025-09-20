# ROS2 RealSense Setup

This repository provides all the commands and instructions to set up Intel RealSense cameras with ROS 2 Humble on Ubuntu 22.04.  
It includes installing system dependencies, librealsense SDK, and the ROS2 RealSense wrapper.  

---

## Prerequisites

- Ubuntu 22.04
- ROS 2 Humble installed ([Installation Guide](https://docs.ros.org/en/humble/Installation.html))

---

## Step 1: Update System & Install Dependencies

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y git cmake build-essential libssl-dev libusb-1.0-0-dev pkg-config libgtk-3-dev

Step 2: Source ROS2 Environment
source /opt/ros/humble/setup.bash


To source automatically on every terminal:

echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
source ~/.bashrc

Step 3: Install Intel RealSense SDK
sudo apt install -y librealsense2-dev librealsense2-utils librealsense2-dkms

Step 4: Create ROS2 Workspace
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws/src

Step 5: Clone ROS2 RealSense Wrapper
git clone https://github.com/IntelRealSense/realsense-ros.git


Note: Do not use the ros2-development branch if using librealsense 2.56.x, as it may include unsupported streams.

Step 6: Install ROS2 RealSense Packages (Optional but Recommended)
sudo apt install -y ros-humble-realsense2-camera ros-humble-realsense2-camera-msgs

Step 7: Build ROS2 Workspace
cd ~/ros2_ws
rm -rf build install log  # clean build
colcon build --symlink-install
source install/setup.bash


Add to ~/.bashrc to automatically source the workspace on new terminals:

echo "source ~/ros2_ws/install/setup.bash" >> ~/.bashrc
source ~/.bashrc

Step 8: Launch RealSense Node
ros2 launch realsense2_camera rs_launch.py


This will start publishing depth and color streams from your RealSense camera.

Notes

This setup works with Intel RealSense SDK 2.56.x and ROS2 Humble.

For newer features like RS2_STREAM_SAFETY or OCCUPANCY, upgrade librealsense to version 2.57+ and ensure compatibility with the ROS2 wrapper.
