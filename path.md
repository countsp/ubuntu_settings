通常情况下，PATH 环境变量用于指定可执行文件的搜索路径，而 LD_LIBRARY_PATH 用于指定动态链接库（.so 文件）的搜索路径。
---
    export PATH=$PATH:/usr/local/cuda/bin 将 /usr/local/cuda/bin 添加到现有的 PATH 环境变量的末尾。这意味着系统在查找可执行文件时，会先搜索 PATH 中原有的目录，如果没有找到，再搜索 /usr/local/cuda/bin。

    export PATH=/usr/local/cuda/bin:$PATH 将 /usr/local/cuda/bin 添加到现有的 PATH 环境变量的开头。这意味着系统在查找可执行文件时，会先搜索 /usr/local/cuda/bin，如果在这个目录中找到了所需的可执行文件，就不会继续搜索 PATH 中的其他目录。
---
当你使用 pip 安装 Python 包时，包通常会被安装到 Python 的 site-packages 目录中。

如果你在全局环境中安装了 open3d，它可能被安装在类似于 /usr/local/lib/python3.x/dist-packages（Linux）或者 C:\Python3x\Lib\site-packages（Windows）的路径下
