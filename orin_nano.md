[烧写教程]https://blog.csdn.net/sinat_34774688/article/details/132389293

在PC 20.04上安装sdk manager能够安装低版本jetpack(5.1.4)

但在 22.04上只能安装 jetpack >= 6

![image](https://github.com/user-attachments/assets/faad47c5-e2ca-4263-b9d7-f422d2515c65)

**不要勾选host machine**

![image](https://github.com/user-attachments/assets/09719f76-4bab-489e-8991-14dac1b19229)


这部分是需要细心处理的步骤，只要是以下几点：

图上第一个箭头处，必须选择“Manual Setup - Jetson Orin Nano Developer Kit 8GB”；

图下第二个箭头处，选择“NVMe”选项；

在“New Username”框中，输入您要设定用户名(一定不要选择可以会与Linux包名重名的用户名)；

在“New Password”框中，输入您要设定的密码。

全部配置完后，就能点击右下角“Flash”按键，开始为Jetson Orin Nano安装操作系统与基础环境，全部大约10分钟时间，这样就完成第一阶段的操作。

![image](https://github.com/user-attachments/assets/ae2da1a3-bfd1-410a-9e55-75df18ddbc13)
