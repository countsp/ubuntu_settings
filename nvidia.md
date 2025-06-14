[image](https://docs.nvidia.com/deeplearning/tensorrt/support-matrix/index.html)

[orin ref](https://blog.csdn.net/sinat_34774688/article/details/134790187)

[orin opencv ref](https://medium.com/@EricChou711/nvidia-jetson-orin-nano-%E6%89%8B%E6%8A%8A%E6%89%8B%E5%AE%8C%E6%95%B4%E5%AE%89%E8%A3%9D%E6%95%99%E5%AD%B8-pytorch-tensorflow-opencv-cuda%E7%89%88%E6%9C%AC-683271bfaa42)

# reference version

cuda 11.6.0

cudnn 8.4.0.27

tensorrt 8.4.2.4

# find compatiale version

[link](https://blog.csdn.net/Vingnir/article/details/135457691?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522171392841816800225536121%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=171392841816800225536121&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~hot_rank-2-135457691-null-null.142%5Ev100%5Epc_search_result_base5&utm_term=tensorrt%E5%92%8Ccuda%E5%AF%B9%E5%BA%94%E7%89%88%E6%9C%AC&spm=1018.2226.3001.4187)


![Screenshot from 2025-02-20 18-42-16](https://github.com/user-attachments/assets/84b2ef2a-2903-483b-bc79-597e9f1bb7cf)

![Screenshot from 2025-02-20 18-41-53](https://github.com/user-attachments/assets/078201ff-afcf-4eb0-ab2b-0d4bb5608e2d)

# GPU Driver

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
sudo update-initramfs -u
sudo rmmod nouveau( optional )
```
3.执行

```
lsmod | grep nouveau
```

如果没有任何回显，则说明nouveau没有被加载。如果还有东西也不要紧，直接继续后续步骤。

4.查看能够安装的版本( 末尾带 recommended，但是不能是server版本)

```
ubuntu-drivers devices
```

如果没有就

```
sudo apt update
```

5.setting->software&updates->additional drivers安装驱动。选择合适的版本

或者 使用命令 sudo apt install nvidia-driver-535-open 安装，如果太慢ppa换源 (不要安装server版本，没有可视化界面)

```
gedit /etc/apt/sources.list.d
# 将文件中的http://ppa.launchpad.net替换为https://launchpad.proxy.ustclug.org
```

设置密码，如 12345678

```
reboot
````
进入MOK

第二项 Enroll MDK -- continue -- yes -- 输入 password  -- Reboot

```
nvidia-smi
```

---


# cuda安装

ref:

[reference1](https://blog.csdn.net/KRISNAT/article/details/134870009)

[reference2](https://zhuanlan.zhihu.com/p/691711768)

[reference3](https://blog.csdn.net/weixin_37926734/article/details/123033286)

官方链接：[CUDA Toolkit - Free Tools and Training](https://developer.nvidia.com/cuda-toolkit-archive)  https://developer.nvidia.com/cuda-toolkit-archive

如果这不是想要的版本，则滑动滚轮至最下方，找到Archive of Previous CUDA Releases，点击进入选择你想要安装的cuda版本，并选择服务器类型，根据下方显示的Installation Instructions安装cuda即可。

![image](https://github.com/countsp/ubuntu_settings/assets/102967883/e725d68e-e6b4-4f5c-97c1-7b9bf9c440b7)


![image](https://github.com/countsp/ubuntu_settings/assets/102967883/b8487a60-7839-4d4e-a061-c655eb458856)


add command to bashrc
```
export PATH=$PATH:/usr/local/cuda/bin
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib64
export CUDA_HOME=$CUDA_HOME:/usr/local/cuda

cd /usr/local
sudo ln -s ./cuda-12.4/ ./cuda         (软链接换成安装的cuda版本)

```


test
```
source ~/.bashrc
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


# cudnn安装

参考 https://www.zhihu.com/question/269324025/answer/3105264795?utm_id=0

[cudnn 下载地址](https://developer.nvidia.com/rdp/cudnn-archive)

-> 选择 Download cuDNN v8.4.0 (April 1st, 2022), for CUDA 11.x

-> 选择 Local Installers for Windows and Linux, Ubuntu(x86_64, armsbsa)

-> 选择 Local Installer for Linux x86_64 (Tar)    // use tar recommended

[直接下载地址 download link]([https://developer.download.nvidia.com/compute/cudnn/secure/8.9.7/local_installers/11.x/cudnn-linux-x86_64-8.9.7.29_cuda11-archive.tar.xz?hHvyX3EPrUBxJSK7mPVcUAQ_-rETyJeNMoemZJIY5BuJZUeZ2gSsv4OpUXWhuMFNHHS4mrC-0Wl2HC_543b-7xpZsQV8vb3sY_xwD2wKEvAPgtk796O5oCdZGDefANDfDS2yinDYLhqhyLqzvwS3Qfncit6jZnAccMrBf5yTpVx6xEZJGdSuAg44X9vqColvMCzG-d0bc11PsPQ7JWulzUg=&t=eyJscyI6IndlYnNpdGUiLCJsc2QiOiJsaW5rLnpoaWh1LmNvbS8/dGFyZ2V0PWh0dHBzJTNBLy9kZXZlbG9wZXIubnZpZGlhLmNvbS9jdWRhLXRvb2xraXQtYXJjaGl2ZSJ9](https://developer.nvidia.com/compute/cudnn/secure/8.4.0/local_installers/11.6/cudnn-linux-x86_64-8.4.0.27_cuda11.6-archive.tar.xz))

-> 手动解压

需要将两组文件复制到cuda目录下

```
sudo cp cudnn-linux-x86_64-8.9.7.29_cuda11-archive/include/* /usr/local/cuda-12.4/include

sudo cp cudnn-linux-x86_64-8.9.7.29_cuda11-archive/lib/libcudnn* /usr/local/cuda-12.4/lib64

```

添加读取权限

```
sudo chmod a+r /usr/local/cuda-12.4/include/cudnn.h
sudo chmod a+r /usr/local/cuda-12.4/lib64/libcudnn*
```

拷贝完成后，我们可以使用如下的命令查看cuDNN的信息：

```
cat /usr/local/cuda-11.6/include/cudnn_version.h | grep CUDNN_MAJOR -A 2
```

![Screenshot from 2024-06-25 10-08-51](https://github.com/countsp/ubuntu_settings/assets/102967883/3155f211-8274-4968-90e0-db89b3c2073b)

---

# tensorRT安装

[Ref](https://blog.csdn.net/m0_60657960/article/details/134770397)\

[official](https://docs.nvidia.com/deeplearning/tensorrt/latest/installing-tensorrt/installing.html)

Check for support version!

[tensorrt support version](https://docs.nvidia.com/deeplearning/tensorrt/support-matrix/index.html)
![image](https://github.com/countsp/ubuntu_settings/assets/102967883/5e4282b5-47a3-452d-b164-fdac6913a78f)


[tensorRT 8.x 下载地址](https://developer.nvidia.com/nvidia-tensorrt-8x-download)

-> 选择 TensorRT 8.4 GA Update 1

-> 选择 TensorRT 8.4 GA Update 1 for Linux x86_64 and CUDA 11.0, 11.1, 11.2, 11.3, 11.4, 11.5, 11.6 and 11.7 TAR Package

[直接下载地址 download link]([https://developer.download.nvidia.com/compute/machine-learning/tensorrt/secure/8.4.2/tars/TensorRT-8.4.2.4.Linux.x86_64-gnu.cuda-11.6.cudnn8.4.tar.gz?qHxQ2C0i2WNJ8xRgMLOTT-vwQFG6oFYRROv9ybqjwiGAgv76dsgFy8Y58DXoGHhQcwqoxX3ItYombc7nvA2_902ZUwDWmvEdQu1Qf7mvOQ04JVe-cZ7cl30fLoQNBBvcvIy34WHr28CwlUtsCCH47KaOCK-Yfftufa20mhBZ_CyKYOY8N9svdCUR6oqS5KiZHhztw9jF-QHbPgK9fc0u9y87Sv_MOdaa4p-xiO2u&t=eyJscyI6IndlYnNpdGUiLCJsc2QiOiJsaW5rLnpoaWh1LmNvbS8/dGFyZ2V0PWh0dHBzJTNBLy9kZXZlbG9wZXIubnZpZGlhLmNvbS9jdWRhLXRvb2xraXQtYXJjaGl2ZSJ9](https://developer.nvidia.com/compute/machine-learning/tensorrt/secure/8.4.2/tars/tensorrt-8.4.2.4.linux.x86_64-gnu.cuda-11.6.cudnn8.4.tar.gz))

```
tar -zxvf TensorRT-8.4.2.4.Linux.x86_64-gnu.cuda-11.6.cudnn8.4.tar.gz
```


add to bashrc
```
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/chopin-aigo-2004/driver/TensorRT-8.4.2.4/lib
```


为了避免其它软件找不到 TensorRT 的库，建议把 TensorRT 的库和头文件添加到系统路径下
```
    # TensorRT路径下
    sudo cp -r ./lib/* /usr/lib
    sudo cp -r ./include/* /usr/include
```
要使用 python 版本，则使用 pip 安装，执行下边的指令

    # 安装TensorRT
    cd TensorRT-8.6.1.6/python
    pip install tensorrt-8.6.1-cp38-none-linux_x86_64.whl
     
    # 安装UFF,支持tensorflow模型转化
    cd TensorRT-8.6.1.6/uff
    pip install uff-0.6.9-py2.py3-none-any.whl
     
    # 安装graphsurgeon，支持自定义结构
    cd TensorRT-8.6.1.6/graphsurgeon
    pip install graphsurgeon-0.4.6-py2.py3-none-any.whl
    

### verify installation

[Ref](https://blog.51cto.com/u_12870633/6149817)

然后验证安装是否成功，进入到TensorRT-8.5.3.1/samples/sampleOnnxMNIST路径下，执行

```
sudo make

```
编译成功后显示可执行那个文件在如下目录(TensorRT-8.5.3.1/bin)

![image](https://github.com/countsp/ubuntu_settings/assets/102967883/56ae719e-fed9-428a-bb5d-5f3ed9ab04fb)

```
./sample_onnx_mnist
```
运行可执行文件sample_onnx_mnist，如果编译和运行过程都没有问题则说明tensorrt安装成功，运行结果如下

![image](https://github.com/countsp/ubuntu_settings/assets/102967883/01b682ad-f417-40b9-ba22-c8ed869bbc42)





(old version)    
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

# tensorrt cmake问题
```
CMake Error at CMakeLists.txt:7 (find_package):
  By not providing "Findtensorrt_cmake_module.cmake" in CMAKE_MODULE_PATH
  this project has asked CMake to find a package configuration file provided
  by "tensorrt_cmake_module", but CMake did not find one.

  Could not find a package configuration file provided by
  "tensorrt_cmake_module" with any of the following names:

    tensorrt_cmake_moduleConfig.cmake
    tensorrt_cmake_module-config.cmake

  Add the installation prefix of "tensorrt_cmake_module" to CMAKE_PREFIX_PATH
  or set "tensorrt_cmake_module_DIR" to a directory containing one of the
  above files.  If "tensorrt_cmake_module" provides a separate development
  package or SDK, be sure it has been installed.

```
在cmakelist中添加
```
set(TensorRT_DIR "/home/rsp4070tis/Downloads/TensorRT-10.9.0.34")

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include ${TensorRT_DIR}/include)
link_directories($${TensorRT_DIR}/lib) # -L
```
## ps 要求

terminal需要能够运行trtexec

需要加入

```
export PATH=$PATH:/home/office2004/TensorRT/TensorRT-8.6.1.6/bin:$PATH

```
---

# OpenCV 4.8.0 安裝

因為原本內建的 OpenCV 並沒有支援 CUDA，所以需要 Build 一版出來進行安裝

## 先刪除原本內建的 OpenCV

sudo sudo apt-get purge *libopencv*

## 執行 OpenCV sh檔案

    CUDA_ARCH_BIN=8.7 需要事先找出版本

    [src](https://developer.nvidia.com/cuda-gpus)
    
    RTX A4000 CUDA_ARCH_BIN=7.5 

## 新建.sh文件

```
#!/bin/bash
set -e

echo "Installing OpenCV 4.8.0 on your Jetson Nano"

# reveal the CUDA location
cd ~
sudo sh -c "echo '/usr/local/cuda/lib64' >> /etc/ld.so.conf.d/nvidia-tegra.conf"
sudo ldconfig

# install the dependencies
sudo apt-get install -y build-essential cmake git unzip pkg-config zlib1g-dev
sudo apt-get install -y libjpeg-dev libjpeg8-dev libjpeg-turbo8-dev libpng-dev libtiff-dev
sudo apt-get install -y libavcodec-dev libavformat-dev libswscale-dev libglew-dev
sudo apt-get install -y libgtk2.0-dev libgtk-3-dev libcanberra-gtk*
sudo apt-get install -y python3-dev python3-numpy python3-pip
sudo apt-get install -y libxvidcore-dev libx264-dev libgtk-3-dev
sudo apt-get install -y libtbb2 libtbb-dev libdc1394-22-dev libxine2-dev
sudo apt-get install -y gstreamer1.0-tools libv4l-dev v4l-utils qv4l2 
sudo apt-get install -y libgstreamer-plugins-base1.0-dev libgstreamer-plugins-good1.0-dev
sudo apt-get install -y libavresample-dev libvorbis-dev libxine2-dev libtesseract-dev
sudo apt-get install -y libfaac-dev libmp3lame-dev libtheora-dev libpostproc-dev
sudo apt-get install -y libopencore-amrnb-dev libopencore-amrwb-dev
sudo apt-get install -y libopenblas-dev libatlas-base-dev libblas-dev
sudo apt-get install -y liblapack-dev liblapacke-dev libeigen3-dev gfortran
sudo apt-get install -y libhdf5-dev protobuf-compiler
sudo apt-get install -y libprotobuf-dev libgoogle-glog-dev libgflags-dev

# remove old versions or previous builds
cd ~ 
sudo rm -rf opencv*
# download the latest version
git clone --depth=1 https://github.com/opencv/opencv.git
git clone --depth=1 https://github.com/opencv/opencv_contrib.git

# set install dir
cd ~/opencv
mkdir build
cd build

# run cmake
cmake -D CMAKE_BUILD_TYPE=RELEASE \
-D CMAKE_INSTALL_PREFIX=/usr \
-D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib/modules \
-D EIGEN_INCLUDE_PATH=/usr/include/eigen3 \
-D WITH_OPENCL=OFF \
-D WITH_CUDA=ON \
-D CUDA_ARCH_BIN=8.7 \
-D CUDA_ARCH_PTX="" \
-D WITH_CUDNN=ON \
-D WITH_CUBLAS=ON \
-D ENABLE_FAST_MATH=ON \
-D CUDA_FAST_MATH=ON \
-D OPENCV_DNN_CUDA=ON \
-D ENABLE_NEON=ON \
-D WITH_QT=OFF \
-D WITH_OPENMP=ON \
-D BUILD_TIFF=ON \
-D WITH_FFMPEG=ON \
-D WITH_GSTREAMER=ON \
-D WITH_TBB=ON \
-D BUILD_TBB=ON \
-D BUILD_TESTS=OFF \
-D WITH_EIGEN=ON \
-D WITH_V4L=ON \
-D WITH_LIBV4L=ON \
-D WITH_PROTOBUF=ON \
-D OPENCV_ENABLE_NONFREE=ON \
-D INSTALL_C_EXAMPLES=OFF \
-D INSTALL_PYTHON_EXAMPLES=OFF \
-D PYTHON3_PACKAGES_PATH=/usr/lib/python3/dist-packages \
-D OPENCV_GENERATE_PKGCONFIG=ON \
-D BUILD_EXAMPLES=OFF ..

# run make

make -j 

sudo make install
sudo ldconfig

# cleaning (frees 320 MB)
make clean
sudo apt-get update

```
opencv和contrib可以手动下载
## 依照剛剛所儲存的名稱{name} 加入權限，並執行

sudo chmod 755 ./{name}.sh #路徑請依照自己sh檔位置執行
./{name}.sh

## 檢查是否成功安裝 OpenCV ( CUDA 版本)

```
sudo pip3 install jetson-stats
sudo reboot 
jtop
```
![Screenshot from 2024-07-16 15-24-34](https://github.com/user-attachments/assets/71a3f1af-4286-49a2-921d-2ba58999dc9e)



# python 调用 build 安装的 opencv
1.在cmake的 build 目录下查找cv2*.so文件

2. 拷贝到使用python的site-packages目录，移除cv2文件夹。

3. 使用 import cv2; print(cv2.__file__)验证
   
# tz Orin上安装 25.5.28
![Uploading Screenshot from 2025-05-28 15-06-33.png…]()

contrib放在opencv内（在build时候替换绝对路径）

```
mkdir build
cd build

cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local/ -D OPENCV_EXTRA_MODULES_PATH=/home/nvidia/software/opencv-4.6.0/opencv_contrib-4.6.0/modules/ -D WITH_CUDA=ON -D CUDA_ARCH_BIN=8.7 -D CUDA_ARCH_PTX="" -D BUILD_opencv_python3=ON -D ENABLE_FAST_MATH=ON -D CUDA_FAST_MATH=ON -D WITH_CUBLAS=ON -D ENABLE_NEON=ON -D WITH_OPENGL=ON -D WITH_LIBV4L=ON -D WITH_GSTREAMER=ON -D WITH_GSTREAMER_0_10=OFF -D WITH_QT=ON -D CUDA_NVCC_FLAGS="--expt-relaxed-constexpr" -D WITH_TBB=ON -D OPENCV_GENERATE_PKGCONFIG=ON -D WITH_GTK_2_X=ON -D BUILD_TIFF=ON ..


(上车域控)
cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local/ -D OPENCV_EXTRA_MODULES_PATH=/media/nvidia/544d38f6-fb25-4e19-919f-fdffa8c60d2a/opencv-4.6.0/opencv_contrib-4.6.0/modules/ -D WITH_CUDA=ON -D CUDA_ARCH_BIN=8.7 -D CUDA_ARCH_PTX="" -D BUILD_opencv_python3=ON -D PYTHON3_EXECUTABLE=/usr/bin/python3 -D PYTHON3_INCLUDE_DIR=/usr/include/python3.8 -D PYTHON3_LIBRARY=/usr/lib/aarch64-linux-gnu/libpython3.8.so -D PYTHON3_PACKAGES_PATH=/usr/lib/python3/dist_packages -D ENABLE_FAST_MATH=ON -D CUDA_FAST_MATH=ON -D WITH_CUBLAS=ON -D ENABLE_NEON=ON -D WITH_OPENGL=ON -D WITH_LIBV4L=ON -D WITH_GSTREAMER=ON -D WITH_GSTREAMER_0_10=OFF -D WITH_QT=ON -D CUDA_NVCC_FLAGS="--expt-relaxed-constexpr" -D WITH_TBB=ON -D OPENCV_GENERATE_PKGCONFIG=ON -D WITH_GTK_2_X=ON -D BUILD_TIFF=ON ..


make -j8 
sudo make install
```

# tz cv_bridge
```
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/src

git clone https://github.com/ros-perception/vision_opencv.git -b noetic

```
修改 cv_bridge 的 CMakeLists.txt：

```
set(OpenCV_DIR /usr/local/share/opencv4)  # 视你的OpenCV安装位置而定
find_package(OpenCV REQUIRED)
```

```
cd catkin_ws

catkin build cv_bridge

echo 'export LD_LIBRARY_PATH=~/software/cv_bridge/devel/lib:$LD_LIBRARY_PATH' >> ~/.bashrc
source ~/.bashrc
```
