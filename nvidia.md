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
