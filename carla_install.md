# all running under 22.04

https://zhuanlan.zhihu.com/p/686519593

# if libomp.so.5 error:

/home/rsp4070tis/carla/CarlaUE4/Binaries/Linux/CarlaUE4-Linux-Shipping: error while loading shared libraries: libomp.so.5: cannot open shared object file: No such file or directory

rsp4070tis@rsp4070tis-MS-7D17:~$ sudo apt-get install libomp5

# if there is no 'carla-0.9.14-ubuntu-22.04'

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

ubuntu环境下，conda虚拟环境安装一些库，在导入时可能会报类似错误。

```
then 
```
ln -sf /usr/lib/x86_64-linux-gnu/libstdc++.so.6 ${CONDA_PREFIX}/lib/libstdc++.so.6
```

or


sudo cp /usr/lib/x86_64-linux-gnu/libstdc++.so.6替换掉报错的libstdc++.so.6即可。

输入 locate libstdc++.so.6 可以查找文件。

输入 strings libstdc++.so.6|grep GLIBCXX_3.4.30 可以查看该库中是否存在GLIBCXX_3.4.30。缺少其它CXX使用类似方法。 
