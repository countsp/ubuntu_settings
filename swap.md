### 如果系统内存不足，可以通过增加交换空间来缓解内存压力。以下是增加 4G 交换空间的步骤：

例如：编译autoware时候遇到 
Error 1
c++: fatal error: Killed signal terminated program cc1plus
compilation terminated.

```
sudo fallocate -l 4G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
sudo swapon --show
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
```
