# carto installation

guide at [https://google-cartographer-ros.readthedocs.io/en/latest/compilation.html](https://google-cartographer-ros.readthedocs.io/en/latest/compilation.html)

Up until this point everything worked fine, but when I try the next step
```
rosdep install --from-paths src --ignore-src --rosdistro=${ROS_DISTRO} -y
```
I get the following error message:

ERROR: the following packages/stacks could not have their rosdep keys resolved to system dependencies: cartographer: [libabsl-dev] defined as "not available" for OS version [focal] 

solve:[https://github.com/cartographer-project/cartographer_ros/issues/1726]

You have to remove (delete/comment out, whatever floats your goat) line 46 (<depend>libabsl-dev</depend>) from the package.xml file in the cartographer (not cartographer ros!) package.
