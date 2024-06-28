# sudo apt update 遇到问题

E: Could not get lock /var/lib/apt/lists/lock. It is held by process 3734 (packagekitd)
N: Be aware that removing the lock file is not a solution and may break your system.
E: Unable to lock directory /var/lib/apt/lists/

![Screenshot from 2024-06-28 11-11-28](https://github.com/countsp/ubuntu_settings/assets/102967883/d7f7325d-16ed-47fd-887c-aa25aeaa962b)

为另一个进程正在使用 apt 系统数据库。通常这是因为有一个自动更新进程正在运行。

**步骤 1：**查找并终止占用 apt 的进程

使用 ps 命令查找占用 apt 系统数据库的进程，然后终止该进程：

```
ps aux | grep -i apt
ps aux | grep -i packagekit
```

找到相关进程的 PID（进程ID），然后使用 kill 命令终止它：

```
sudo kill -9 <PID>
```

例如，如果 packagekitd 的 PID 是 3734，你可以使用以下命令终止它：

```
sudo kill -9 3734
```
