1.在安装NVIDIA驱动时，需要禁用nouveau驱动才可以。
禁用方法如下：
```
sudo gedit  /etc/modprobe.d/blacklist.conf
```
在文件的尾部追加两行
```
blacklist nouveau
options nouveau modeset=0
```

2.保存退出后，执行
```
update-initramfs -u
rmmod nouveau( optional )
```
3.执行

```
lsmod | grep nouveau
```

如果没有任何回显，则说明nouveau没有被加载。

4.
```
ubuntu-drivers devices
```
check for suitable driver version (ending with recommended)

5.setting->software&updates->additional drivers安装驱动。选择合适的版本

或者 使用命令 sudo apt install nvidia-driver-535-server-open 安装，如果太慢ppa换源

```
gedit /etc/apt/sources.list.d
# 将文件中的http://ppa.launchpad.net替换为https://launchpad.proxy.ustclug.org
```

设置密码，如 12345678

```
reboot
````
进入MOK

select 第二项 enter 输入 password

再reboot

```
nvidia-smi
```

---


#### cuda安装

官方链接：[CUDA Toolkit - Free Tools and Training](https://developer.nvidia.com/cuda-toolkit-archive)  https://developer.nvidia.com/cuda-toolkit-archive

如果这不是想要的版本，则滑动滚轮至最下方，找到Archive of Previous CUDA Releases，点击进入选择你想要安装的cuda版本，并选择服务器类型，根据下方显示的Installation Instructions安装cuda即可。

![image](https://github.com/countsp/ubuntu_settings/assets/102967883/e725d68e-e6b4-4f5c-97c1-7b9bf9c440b7)


![image](https://github.com/countsp/ubuntu_settings/assets/102967883/b8487a60-7839-4d4e-a061-c655eb458856)


add command to bashrc
```
export PATH=$PATH:/usr/local/cuda-11.8/bin
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda-11.8/lib64
export CUDA_HOME=$CUDA_HOME:/usr/local/cuda-11.8
```


test
```
nvcc -V 
```
```
输出
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2021 NVIDIA Corporation
Built on Fri_Dec_17_18:16:03_PST_2021
Cuda compilation tools, release 11.6, V11.6.55
Build cuda_11.6.r11.6/compiler.30794723_0

```


old version (optional)
```
wget https://developer.download.nvidia.com/compute/cuda/11.6.0/local_installers/cuda_11.6.0_510.39.01_linux.run
sudo sh cuda_11.6.0_510.39.01_linux.run
```

```
===========
= Summary =
===========

Driver:   Not Selected
Toolkit:  Installed in /usr/local/cuda-11.6/

Please make sure that
 -   PATH includes /usr/local/cuda-11.6/bin
 -   LD_LIBRARY_PATH includes /usr/local/cuda-11.6/lib64, or, add /usr/local/cuda-11.6/lib64 to /etc/ld.so.conf and run ldconfig as root

To uninstall the CUDA Toolkit, run cuda-uninstaller in /usr/local/cuda-11.6/bin
***WARNING: Incomplete installation! This installation did not install the CUDA Driver. A driver of version at least 510.00 is required for CUDA 11.6 functionality to work.
To install the driver using this installer, run the following command, replacing <CudaInstaller> with the name of this run file:
    sudo <CudaInstaller>.run --silent --driver

Logfile is /var/log/cuda-installer.log
```



#### cuda 卸载

https://blog.csdn.net/weixin_37926734/article/details/123033286

---
#### cudnn安装
参考 https://www.zhihu.com/question/269324025/answer/3105264795?utm_id=0

[cudnn 下载地址](https://developer.nvidia.com/rdp/cudnn-archive)

-> 选择 Download cuDNN v8.4.0 (April 1st, 2022), for CUDA 11.x

-> 选择 Local Installers for Windows and Linux, Ubuntu(x86_64, armsbsa)

-> 选择 Local Installer for Linux x86_64 (Tar)

[直接下载地址 download link](https://developer.download.nvidia.com/compute/cudnn/secure/8.9.7/local_installers/11.x/cudnn-linux-x86_64-8.9.7.29_cuda11-archive.tar.xz?hHvyX3EPrUBxJSK7mPVcUAQ_-rETyJeNMoemZJIY5BuJZUeZ2gSsv4OpUXWhuMFNHHS4mrC-0Wl2HC_543b-7xpZsQV8vb3sY_xwD2wKEvAPgtk796O5oCdZGDefANDfDS2yinDYLhqhyLqzvwS3Qfncit6jZnAccMrBf5yTpVx6xEZJGdSuAg44X9vqColvMCzG-d0bc11PsPQ7JWulzUg=&t=eyJscyI6IndlYnNpdGUiLCJsc2QiOiJsaW5rLnpoaWh1LmNvbS8/dGFyZ2V0PWh0dHBzJTNBLy9kZXZlbG9wZXIubnZpZGlhLmNvbS9jdWRhLXRvb2xraXQtYXJjaGl2ZSJ9)



需要将两组文件复制到cuda目录下

[reference](https://blog.csdn.net/weixin_37926734/article/details/123033286)
```
cp cuda/lib64/* /usr/local/cuda-11.6/lib64/
cp cuda/include/* /usr/local/cuda-11.6/include/
```


拷贝完成后，我们可以使用如下的命令查看cuDNN的信息：

```
cat /usr/local/cuda-11include/cudnn_version.h | grep CUDNN_MAJOR -A 2
```
---

#### tensorRT安装
[tensorRT 8.x 下载地址](https://developer.nvidia.com/nvidia-tensorrt-8x-download)

-> 选择 TensorRT 8.4 GA Update 1

-> 选择 TensorRT 8.4 GA Update 1 for Linux x86_64 and CUDA 11.0, 11.1, 11.2, 11.3, 11.4, 11.5, 11.6 and 11.7 TAR Package

[直接下载地址 download link](https://developer.download.nvidia.com/compute/machine-learning/tensorrt/secure/8.4.2/tars/TensorRT-8.4.2.4.Linux.x86_64-gnu.cuda-11.6.cudnn8.4.tar.gz?qHxQ2C0i2WNJ8xRgMLOTT-vwQFG6oFYRROv9ybqjwiGAgv76dsgFy8Y58DXoGHhQcwqoxX3ItYombc7nvA2_902ZUwDWmvEdQu1Qf7mvOQ04JVe-cZ7cl30fLoQNBBvcvIy34WHr28CwlUtsCCH47KaOCK-Yfftufa20mhBZ_CyKYOY8N9svdCUR6oqS5KiZHhztw9jF-QHbPgK9fc0u9y87Sv_MOdaa4p-xiO2u&t=eyJscyI6IndlYnNpdGUiLCJsc2QiOiJsaW5rLnpoaWh1LmNvbS8/dGFyZ2V0PWh0dHBzJTNBLy9kZXZlbG9wZXIubnZpZGlhLmNvbS9jdWRhLXRvb2xraXQtYXJjaGl2ZSJ9)

```
tar -zxvf TensorRT-8.4.2.4.Linux.x86_64-gnu.cuda-11.6.cudnn8.4.tar.gz
export TENSORRT_DIR=$(pwd)/TensorRT-8.4.2.4
cd TensorRT-8.4.2.4/python
python3 -V# pip install tensorrt-8.4.2.4-cp38-none-linux_x86_64.whl
export LD_LIBRARY_PATH=/home/chopin/Downloads/TensorRT-8.4.2.4/targets/x86_64-linux-gnu/lib:$LD_LIBRARY_PATH
python3
import tensorrt

```

chopin@chopin-HP-Z2-Tower-G9-Workstation-Desktop-PC:~/TensorRT-8.4.2.4/TensorRT-8.4.2.4$ sudo cp -r ./lib/* /usr/lib
chopin@chopin-HP-Z2-Tower-G9-Workstation-Desktop-PC:~/TensorRT-8.4.2.4/TensorRT-8.4.2.4$ sudo cp -r ./include/* /usr/include
```
pip3 install tensorrt-8.4.2.4-cp38-none-linux_x86_64.whl 
pip3 install graphsurgeon-0.4.6-py2.py3-none-any.whl
```

https://blog.51cto.com/u_12870633/6149817
