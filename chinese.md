# 中文输入法设置
summarzied from [guide](https://blog.csdn.net/qq_29750461/article/details/128347231)
其中重启可以使用ibus restart代替

1.settings

2.页面左侧的导航栏中选择“Region&Language”，然后在右侧页面中点击“Manage Install Languages”。

3.如果弹出窗口Language support not installed properly，单击 Install，然后等待安装完毕。

4.单击“Install/Remove Languages”。

5.勾选Chinese(simplified)，然后单击Apply，开始装简体中文

6.安装中文语言包

```
sudo apt-get update 
sudo apt-get install language-pack-zh-hans
```

7.安装输入法
```
sudo apt install ibus-libpinyin
sudo apt install ibus-clutter
```

8.重启电脑或者
```
ibus restart
```

9.Settings -- Region and Language -- Input Sources  --  +

选择 chinese 选 chinese (intelligent pinyin) 中文智能拼音

如果没有应该是没有重启


# 22.04
[看这个链接设置](https://blog.csdn.net/liutuoqi123/article/details/140596599)

sudo apt update
sudo apt install language-pack-zh-hans
sudo apt install ibus ibus-libpinyin



打开“设置”应用，找到“区域与语言”或类似选项。

确保已添加并启用中文（简体）语言。

进入“输入源”或“键盘输入法”设置，点击“+”添加新输入源，搜索并选择“汉语（简体）- IBus”下的某个中文输入法，如“IBus Pinyin”。


ibus-setup
