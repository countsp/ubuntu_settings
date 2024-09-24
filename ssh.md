在同一个Wi-Fi网络下的两个Ubuntu设备之间传文件有多种方法，以下是几种常见的解决方案：
1. 使用SSH和SCP传输

如果两台设备已经设置了SSH，你可以使用SCP命令进行文件传输。

步骤：

确保两台设备都安装了SSH：
```
sudo apt update
sudo apt install openssh-server
```

在发送文件的设备上，使用以下命令将文件传输到目标设备：

```
scp /path/to/local/file username@remote_ip:/path/to/remote/directory
```

例如：

```
scp ~/Documents/file.txt user@192.168.1.10:~/Documents/
```
