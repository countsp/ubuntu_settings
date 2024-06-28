# sudo ldconfig时报错

![Screenshot from 2024-06-28 08-46-48](https://github.com/countsp/ubuntu_settings/assets/102967883/ee6e4bc1-5d7c-48b8-8758-ea937ea70bcb)


**步骤 1：** 备份原始文件

首先，备份这些库文件以防操作失误：
```
cd /usr/local/cuda/targets/x86_64-linux/lib/

sudo cp libcudnn_cnn_train.so.8 libcudnn_cnn_train.so.8.bak
sudo cp libcudnn_ops_train.so.8 libcudnn_ops_train.so.8.bak
sudo cp libcudnn_adv_train.so.8 libcudnn_adv_train.so.8.bak
sudo cp libcudnn.so.8 libcudnn.so.8.bak
sudo cp libcudnn_ops_infer.so.8 libcudnn_ops_infer.so.8.bak
sudo cp libcudnn_cnn_infer.so.8 libcudnn_cnn_infer.so.8.bak
sudo cp libcudnn_adv_infer.so.8 libcudnn_adv_infer.so.8.bak
```

**步骤 2：** 删除原始文件并创建符号链接

然后，删除原始文件并为其创建符号链接：

```
sudo rm libcudnn_cnn_train.so.8
sudo rm libcudnn_ops_train.so.8
sudo rm libcudnn_adv_train.so.8
sudo rm libcudnn.so.8
sudo rm libcudnn_ops_infer.so.8
sudo rm libcudnn_cnn_infer.so.8
sudo rm libcudnn_adv_infer.so.8
```

```
sudo ln -s libcudnn_cnn_train.so.8.x.x.x libcudnn_cnn_train.so.8
sudo ln -s libcudnn_ops_train.so.8.x.x.x libcudnn_ops_train.so.8
sudo ln -s libcudnn_adv_train.so.8.x.x.x libcudnn_adv_train.so.8
sudo ln -s libcudnn.so.8.x.x.x libcudnn.so.8
sudo ln -s libcudnn_ops_infer.so.8.x.x.x libcudnn_ops_infer.so.8
sudo ln -s libcudnn_cnn_infer.so.8.x.x.x libcudnn_cnn_infer.so.8
sudo ln -s libcudnn_adv_infer.so.8.x.x.x libcudnn_adv_infer.so.8
```


将 8.x.x.x 替换为实际的版本号，例如 8.2.2.26。确认实际版本号可以通过以下命令查看目录内容：

```
ls -l /usr/local/cuda/targets/x86_64-linux/lib/
```

**步骤 3：** 重新运行 ldconfig

完成上述步骤后，重新运行 ldconfig 命令：

```
sudo ldconfig
```
