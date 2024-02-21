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
rmmod nouveau
```
3.重启系统，执行

```
root@Test#lsmod | grep nouveau
```

如果没有任何回显，则说明nouveau没有被加载。
```
ubuntu-drivers devices
```
check for suitable driver version

5.setting->software&updates->additional drivers安装驱动。选择合适的版本

设置密码，如 12345678
```
reboot
````
进入第二项 进入第一/第二项？ 输入 password

再reboot

```
nvidia-smi
```

---


#### cuda安装
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
---
#### cudnn安装
参考 https://www.zhihu.com/question/269324025/answer/3105264795?utm_id=0

[cudnn 下载地址](https://developer.nvidia.com/rdp/cudnn-archive)

-> 选择 Download cuDNN v8.9.7 (December 5th, 2023), for CUDA 11.x

-> 选择 Local Installers for Windows and Linux, Ubuntu(x86_64, armsbsa)

-> 选择 Local Installer for Linux x86_64 (Tar)

[直接下载地址 download link](https://developer.download.nvidia.com/compute/cudnn/secure/8.9.7/local_installers/11.x/cudnn-linux-x86_64-8.9.7.29_cuda11-archive.tar.xz?hHvyX3EPrUBxJSK7mPVcUAQ_-rETyJeNMoemZJIY5BuJZUeZ2gSsv4OpUXWhuMFNHHS4mrC-0Wl2HC_543b-7xpZsQV8vb3sY_xwD2wKEvAPgtk796O5oCdZGDefANDfDS2yinDYLhqhyLqzvwS3Qfncit6jZnAccMrBf5yTpVx6xEZJGdSuAg44X9vqColvMCzG-d0bc11PsPQ7JWulzUg=&t=eyJscyI6IndlYnNpdGUiLCJsc2QiOiJsaW5rLnpoaWh1LmNvbS8/dGFyZ2V0PWh0dHBzJTNBLy9kZXZlbG9wZXIubnZpZGlhLmNvbS9jdWRhLXRvb2xraXQtYXJjaGl2ZSJ9)

---

#### tensorRT安装
[tensorRT 8.x 下载地址](https://developer.nvidia.com/nvidia-tensorrt-8x-download)

-> 选择 TensorRT 8.4 GA Update 1

-> 选择 TensorRT 8.4 GA Update 1 for Linux x86_64 and CUDA 11.0, 11.1, 11.2, 11.3, 11.4, 11.5, 11.6 and 11.7 TAR Package

[直接下载地址 download link](https://developer.download.nvidia.com/compute/machine-learning/tensorrt/secure/8.4.2/tars/TensorRT-8.4.2.4.Linux.x86_64-gnu.cuda-11.6.cudnn8.4.tar.gz?qHxQ2C0i2WNJ8xRgMLOTT-vwQFG6oFYRROv9ybqjwiGAgv76dsgFy8Y58DXoGHhQcwqoxX3ItYombc7nvA2_902ZUwDWmvEdQu1Qf7mvOQ04JVe-cZ7cl30fLoQNBBvcvIy34WHr28CwlUtsCCH47KaOCK-Yfftufa20mhBZ_CyKYOY8N9svdCUR6oqS5KiZHhztw9jF-QHbPgK9fc0u9y87Sv_MOdaa4p-xiO2u&t=eyJscyI6IndlYnNpdGUiLCJsc2QiOiJsaW5rLnpoaWh1LmNvbS8/dGFyZ2V0PWh0dHBzJTNBLy9kZXZlbG9wZXIubnZpZGlhLmNvbS9jdWRhLXRvb2xraXQtYXJjaGl2ZSJ9)

```
tar -zxvf TensorRT-8.4.2.4.Linux.x86_64-gnu.cuda-11.6.cudnn8.4.tar.gz
# export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:<TensorRT-$8.4.2.4/lib>
export TENSORRT_DIR=$(pwd)/TensorRT-8.4.2.4
cd TensorRT-8.4.2.4/python
python3 -V# pip install tensorrt-8.4.2.4-cp38-none-linux_x86_64.whl
export LD_LIBRARY_PATH=/home/chopin/Downloads/TensorRT-8.4.2.4/targets/x86_64-linux-gnu/lib:$LD_LIBRARY_PATH
 python3import tensorrt

```
