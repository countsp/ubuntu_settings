# Ros installation

summarzied from [guide](https://linux.how2shout.com/learn-ros-noetic-installation-on-ubuntu-20-04-lts/)

```
sudo apt update && sudo apt upgrade
sudo apt install curl -y
```
#### Add ROS Noetic package repository
```
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
```
#### Add ROS Noetic key
```
curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -

sudo apt update
```
#### Install ROS Noetic
sudo apt install ros-noetic-desktop-full

#### Source before use
echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
source ~/.bashrc

#### Rosdep command
sudo rosdep init
sudo rosdep fix-permissions
