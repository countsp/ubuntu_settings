# all running under 22.04

https://zhuanlan.zhihu.com/p/686519593

# if libomp.so.5 error:

/home/rsp4070tis/carla/CarlaUE4/Binaries/Linux/CarlaUE4-Linux-Shipping: error while loading shared libraries: libomp.so.5: cannot open shared object file: No such file or directory

rsp4070tis@rsp4070tis-MS-7D17:~$ sudo apt-get install libomp5

# if there is no 'carla-0.9.14-cp310-cp310-linux_x86_64.whl '

https://github.com/gezp/carla_ros/releases/tag/carla-0.9.14-ubuntu-22.04

download here

# if black screen running

```
sh ~/carla/CarlaUE4.sh
```

install gpu driver first

# if GLIBCXX error
```
(carla) rsp4070tis@rsp4070tis-MS-7D17:~/carla/PythonAPI/examples$ python manual_control.py 
Traceback (most recent call last):
  File "/home/rsp4070tis/carla/PythonAPI/examples/manual_control.py", line 83, in <module>
    import carla
  File "/home/rsp4070tis/anaconda3/envs/carla/lib/python3.10/site-packages/carla/__init__.py", line 8, in <module>
    from .libcarla import *
ImportError: /home/rsp4070tis/anaconda3/envs/carla/bin/../lib/libstdc++.so.6: version `GLIBCXX_3.4.30' not found (required by /home/rsp4070tis/anaconda3/envs/carla/lib/python3.10/site-packages/carla/libcarla.cpython-310-x86_64-linux-gnu.so)
```
ubuntu环境下，conda虚拟环境安装一些库，在导入时可能会报类似错误。

 
```
ln -sf /usr/lib/x86_64-linux-gnu/libstdc++.so.6 ${CONDA_PREFIX}/lib/libstdc++.so.6
```

or


sudo cp /usr/lib/x86_64-linux-gnu/libstdc++.so.6替换掉报错的libstdc++.so.6即可。

输入 locate libstdc++.so.6 可以查找文件。

输入 strings libstdc++.so.6|grep GLIBCXX_3.4.30 可以查看该库中是否存在GLIBCXX_3.4.30。缺少其它CXX使用类似方法。 

# shapely
pip install pygame

pip install shapely

pip install networkx

pip install numpy


# all running under 20.04

## autoware install

https://zhuanlan.zhihu.com/p/613127230

## carla install

https://blog.csdn.net/wenquantongxin/article/details/142625286

# 错误修正帖

[error](https://zhuanlan.zhihu.com/p/12329118060)

## error Could not find a connection between 'map' and 'base_link' because they are not part of the same tree.Tf

需要修改的地方：carla_pointcloud_interface_node.cpp

改为true后，会启用点云转换并发布不同的topic（详见源代码）

PointCloudInterface::PointCloudInterface(const rclcpp::NodeOptions & node_options)
: Node("carla_pointcloud_interface_node", node_options), 
tf_output_frame_("base_link"), b_create_ex_(true)  //将此处的默认参数b_create_ex_(false) 改为 true

修改位置2 、 3：此处主要是将点云发布到veloodyne_top这个 tf坐标系下

    {
      auto ros_pc_msg_ptr = std::make_unique<sensor_msgs::msg::PointCloud2>();
      pcl::toROSMsg(*valid_points_xyzir, *ros_pc_msg_ptr);
      ros_pc_msg_ptr->header.frame_id = "velodyne_top";    //此处由seneor_kit_base_link修改为velodyne_top
      velodyne_points_pub_->publish(std::move(ros_pc_msg_ptr));
    }

    ...(省略中间未修改的地方)

    {//这是下面另一部分的Publish的代码，同样修改
      auto ros_pc_ex_msg_ptr = std::make_unique<sensor_msgs::msg::PointCloud2>();
      pcl::toROSMsg(*valid_points_xyziradt, *ros_pc_ex_msg_ptr);

      ros_pc_ex_msg_ptr->header.frame_id = "velodyne_top";//此处由seneor_kit_base_link修改为velodyne_top
      velodyne_points_ex_pub_->publish(std::move(ros_pc_ex_msg_ptr));
    }
