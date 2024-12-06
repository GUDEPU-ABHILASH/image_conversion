# Image Conversion Package for ROS 2

This repository contains the `image_conversion_pkg`, a ROS 2 package designed to demonstrate image processing using OpenCV and ROS 2's `image_transport`. The package subscribes to an image topic, processes the image (e.g., converts it to grayscale), and displays it using OpenCV.

## Table of Contents

1. [Prerequisites](#prerequisites)  
2. [Step-by-Step Procedure for Creating the Workspace](#step-by-step-procedure-for-creating-the-workspace)  
   - [Create the Workspace](#create-the-workspace)  
   - [Clone the Repository](#clone-the-repository)   
   - [Build the Package](#build-the-package)  
3. [Repository Structure](#repository-structure)  
4. [Run the Node](#run-the-node)  
5. [Check the Results](#check-the-results)

## Prerequisites

Before setting up the package, ensure you have the following:

- **ROS 2 Humble Hawksbill** installed. ([Installation Guide](https://docs.ros.org/en/humble/Installation.html))
- **Installation of usb_cam package** 
    ```bash
    sudo apt-get install ros-humble-usb-cam
- OpenCV installed (usually included with `cv_bridge`).  
- `colcon` build tool installed.  
- `image_transport` and `cv_bridge` ROS 2 dependencies.

## Step-by-Step Procedure for creating the workspace
# 1. Create the workspace 
- Create the workspace 
    ```bash
    mkdir -p ~/ros2_ws/src
# 2. Clone the Repository
- Change the path into source directory of the workspace
    ```bash
    cd ~/ros2_ws/src
- Clone the repository from github
    ```bash
    git clone https://github.com/GUDEPU-ABHILASH/image_conversion.git
# 3. Build the Package 
- Change the path to ros2_ws directory
    ```bash
    cd ..
- Build the Package
    ```bash
    colcon build
## Repository Structure

Once cloned and set up, your workspace should look like this:

      ros2_ws/
      ├── src/
      │   └── image_conversion_pkg/
      │       ├── CMakeLists.txt
      │       ├── package.xml
      │       └── src/
      │           └── image_converter_node.cpp
              └── launch
                  └── image_conversion_launch.py
      ├── build/
      ├── install/
      └── log/

## Run the Node
- Open a terminal and source the workspace
    ```bash
    source ~/ros2_ws/install/setup.bash
- Launch the image_conversion node with the following command
    ```bash
    ros2 launch image_conversion_pkg image_conversion_launch.py
This will start the image_Conversion node and collects the data from the camera

## Check the results
- Open another terminal and paste the below command
    ```bash
    ros2 run rqt_image_view rqt_image_view
This will open a window which show the feed of /camera
### Mode - 1 (Gray Scale Image)
- To check the gray scale converted image. Use below command
    ```bash
    ros2 service call /set_mode std_srvs/srv/SetBool "{data: true}"
- This is the service which is assigned to change the image feed into the gray scale format
- After entering this command, open the rqt_image_view window and change the drop down to /camera/converted_image

![Screenshot from 2024-12-02 18-30-15](https://github.com/user-attachments/assets/3d35fcf9-69d9-44c7-8421-719e47b1483a)



### Mode - 2 (Coloured Image)
- To change the converted image into Colour, then paste the below command in new terminal
    ```bash
    ros2 service call /set_mode std_srvs/srv/SetBool "{data: false}"
- This is the service which is assigned to change the image feed into the gray scale format
- After entering this command, open the rqt_image_view window and change the drop down to /camera/converted_image


![Screenshot from 2024-12-02 18-28-32](https://github.com/user-attachments/assets/334b383c-f6d4-4deb-a14d-e204f82112f5)
