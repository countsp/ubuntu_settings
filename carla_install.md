22.04

https://zhuanlan.zhihu.com/p/686519593

# if libomp.so.5 error:

/home/rsp4070tis/carla/CarlaUE4/Binaries/Linux/CarlaUE4-Linux-Shipping: error while loading shared libraries: libomp.so.5: cannot open shared object file: No such file or directory

rsp4070tis@rsp4070tis-MS-7D17:~$ sudo apt-get install libomp5

# if black screen running

```
sh ~/carla/CarlaUE4.sh
```

install gpu driver first


if error like this
```
(carla) rsp4070tis@rsp4070tis-MS-7D17:~/carla/PythonAPI/examples$ python manual_control.py 
Traceback (most recent call last):
  File "/home/rsp4070tis/carla/PythonAPI/examples/manual_control.py", line 83, in <module>
    import carla
  File "/home/rsp4070tis/anaconda3/envs/carla/lib/python3.10/site-packages/carla/__init__.py", line 8, in <module>
    from .libcarla import *
ImportError: /home/rsp4070tis/anaconda3/envs/carla/bin/../lib/libstdc++.so.6: version `GLIBCXX_3.4.30' not found (required by /home/rsp4070tis/anaconda3/envs/carla/lib/python3.10/site-packages/carla/libcarla.cpython-310-x86_64-linux-gnu.so)
```
then 
```
ln -sf /usr/lib/x86_64-linux-gnu/libstdc++.so.6 ${CONDA_PREFIX}/lib/libstdc++.so.6
```
