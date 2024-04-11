1.下载ceres-solver-1.14.0

```
wget ceres-solver.org/ceres-solver-1.14.0.tar.gz
```

2.解压

```
tar xvf ceres-solver-1.14.0.tar.gz
```

optional:把名字改成ceres-solver

3.编译

```
cd ceres-solver 
mkdir build 
cd build 
cmake ..
make
sudo make install
```
4.验证
```
bin/simple_bundle_adjuster  ../data/problem-16-22106-pre.txt 
```

![Screenshot from 2024-04-11 01-21-57](https://github.com/countsp/ubuntu_settings/assets/102967883/9c499be6-14eb-4c87-abcf-f0097006de6c)
