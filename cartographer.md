# carto installation

guide at [https://google-cartographer-ros.readthedocs.io/en/latest/compilation.html](https://google-cartographer-ros.readthedocs.io/en/latest/compilation.html)


On Ubuntu Focal with ROS Noetic use these commands to install the above tools:
```
sudo apt-get update
sudo apt-get install -y python3-wstool python3-rosdep ninja-build stow
```

On older distributions:
```
sudo apt-get update
sudo apt-get install -y python-wstool python-rosdep ninja-build stow
```
After the tools are installed, create a new cartographer_ros workspace in ‘catkin_ws’.
```
mkdir catkin_ws
cd catkin_ws
wstool init src
wstool merge -t src https://raw.githubusercontent.com/cartographer-project/cartographer_ros/master/cartographer_ros.rosinstall
wstool update -t src
```
Now you need to install cartographer_ros’ dependencies. First, we use rosdep to install the required packages. The command ‘sudo rosdep init’ will print an error if you have already executed it since installing ROS. This error can be ignored.
```
sudo rosdep init
rosdep update
rosdep install --from-paths src --ignore-src --rosdistro=${ROS_DISTRO} -y
```
Cartographer uses the abseil-cpp library that needs to be manually installed using this script:
```
src/cartographer/scripts/install_abseil.sh
```
Due to conflicting versions you might need to uninstall the ROS abseil-cpp using
```
sudo apt-get remove ros-${ROS_DISTRO}-abseil-cpp
```
Build and install.

```
catkin_make_isolated --install --use-ninja
```


Up until this point everything worked fine, but when I try the next step
```
rosdep install --from-paths src --ignore-src --rosdistro=${ROS_DISTRO} -y
```
I get the following error message:

ERROR: the following packages/stacks could not have their rosdep keys resolved to system dependencies: cartographer: [libabsl-dev] defined as "not available" for OS version [focal] 

solve:[https://github.com/cartographer-project/cartographer_ros/issues/1726]

You have to remove (delete/comment out, whatever floats your goat) line 46 (<depend>libabsl-dev</depend>) from the package.xml file in the cartographer (not cartographer ros!) package.
