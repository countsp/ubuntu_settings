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