# FlightGoggles

## Installation for Ubuntu 18.04 (Bionic)

This is a fork of MIT-fast's FlightGoggles repo with an walkthrough about installing it on Ubuntu 18.04.

Install ROS Melodic

Do not use ROS Kinetic as it does not support Bionic.

```bash
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116
sudo apt update
sudo apt install ros-melodic-desktop-full
```
Install FlightGoggles

Copied from [here](https://github.com/mit-fast/FlightGoggles/wiki/installation-local). A few changes are made to work with melodic.

```bash
# Setup catkin workspace
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/
catkin config --extend /opt/ros/melodic
catkin init
# Add workspace to bashrc.
echo 'source ~/catkin_ws/devel/setup.bash' >> ~/.bashrc
cd src
wstool init
# Install FlightGoggles nodes and deps from rosinstall file
wstool merge https://raw.githubusercontent.com/chuanli11/FlightGoggles/master/flightgoggles.rosinstall
wstool update
cd ../
# Install required libraries.
rosdep install --from-paths src --ignore-src --rosdistro melodic -y
# Install external libraries for flightgoggles_ros_bridge
sudo apt install -y libzmqpp-dev libeigen3-dev
# Install dependencies for flightgoggles renderer
sudo apt install -y libvulkan1 mesa-vulkan-drivers vulkan-tools
# Build nodes
catkin build
# Refresh workspace
source ~/.bashrc
```
Run
```bash
# To run example environment with joystick/keyboard teleoperation
roslaunch flightgoggles teleopExample.launch

# See this link for control with keyboard
https://github.com/mit-fast/FlightGoggles/wiki/Default-Controls
```


## Documentation, Installation, & Usage Instructions
Please refer to the [wiki-page](https://github.com/mit-fast/FlightGoggles/wiki) for code documentation, installation, usage instructions. An [FAQ](https://github.com/mit-fast/FlightGoggles/wiki/FAQ) is also available there.

## Description

A framework for photorealistic hardware-in-the-loop agile flight simulation using Unity3D and ROS.

[![Video Link](Images/Abandoned_Factory_2.jpg)](https://youtu.be/e_3Yw0uPRKE)

![](Images/Abandoned_Factory25.jpg)



## Citation
If you find this work useful for your research, please cite:
```bibtex
@inproceedings{sayremccord2018visual,
  title={Visual-inertial navigation algorithm development using photorealistic camera simulation in the loop},
  author={Sayre-McCord, Thomas and
  Guerra, Winter and
  Antonini, Amado and
  Arneberg, Jasper and
  Brown, Austin and
  Cavalheiro, Guilherme and
  Fang, Yajun and
  Gorodetsky, Alex and
  McCoy, Dave and
  Quilter, Sebastian and
  Riether, Fabian and
  Tal, Ezra and
  Terzioglu, Yunus and
  Carlone, Luca and
  Karaman, Sertac},
  booktitle={2018 IEEE International Conference on Robotics and Automation (ICRA)},
  year={2018}
}
```
## Papers using this work
```bibtex
@inproceedings{antonini2018blackbird,
  title={The Blackbird Dataset: A large-scale dataset for UAV perception in aggressive flight},
  author={Antonini, Amado and Guerra, Winter and Murali, Varun and Sayre-McCord, Thomas and Karaman, Sertac},
  booktitle={International Symposium on Experimental Robotics, {ISER} 2018, Buenos Aires,
               Argentina, November 5-8, 2018.},
  year={2018}
}
```
Blackbird Dataset: [Paper](https://arxiv.org/abs/1810.01987) [Website](https://github.com/mit-fast/Blackbird-Dataset)

## Core Contributers

```
Winter Guerra
Ezra Tal
Varun Murali
Sebastian Quilter
John Aleman
Sertac Karaman
```
