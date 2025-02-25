[source](https://blog.csdn.net/zhngyue123/article/details/133900617?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ECtr-1-133900617-blog-129943471.235%5Ev43%5Epc_blog_bottom_relevance_base6&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ECtr-1-133900617-blog-129943471.235%5Ev43%5Epc_blog_bottom_relevance_base6&utm_relevant_index=2)

ROS2的cv_bridge和opencv版本不匹配问题

1. 问题
```
/usr/bin/ld: warning: libopencv_imgcodecs.so.4.2, needed by /opt/ros/foxy/lib/libcv_bridge.so, may conflict with libopencv_imgcodecs.so.4.5   
/usr/bin/ld: warning: libopencv_core.so.4.2, needed by /opt/ros/foxy/lib/libcv_bridge.so, may conflict with libopencv_core.so.4.5
```

2. 原因

   ros安装的时候默认的opencv版本是4.2,和本地安装的opencv版本不匹配(我的本地安装的是4.5)

3. 解决方案

    单独重新安装cv_bridge库

    //下载对应版本的cv_bridge包(我安装的foxy)
     
    $ git clone https://github.com/ros-perception/vision_opencv.git -b foxy

    //进入cv_bridge目录,
     
    //修改CMakeLists.txt文件的opencv版本号,
     
    //改成自己本地安装的版本
     
     
    find_package(OpenCV 4 QUIET // 改成find_package(OpenCV 4.5 QUIET
     
    COMPONENTS
     
    opencv_core
     
    opencv_imgproc
     
    opencv_imgcodecs
     
    CONFIG
     
    )

    //编译的时候指定安装路径(ros2安装的目录下,我的ros2安装目录:/opt/ros/foxy)
     
    $ cd vision_opencv/cv_bridge
     
    $ mkdir build && cd build
     
    $ cmake -DCMAKE_INSTALL_PREFIX=/opt/ros/foxy ..
     
    $ sudo make install

# 查看opencv路径
pkg-config --cflags --libs opencv4

# 查看opencv路径版本
opencv_version
