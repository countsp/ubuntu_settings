# Error: GTSAM was built against a different version of Eigen。

这个问题是GTSAM自带的eigen库和之前安装的eigen库的版本不同导致的。

**解决办法：**
修改gtsam下的CMakeLists.txt文件中的内容，在if(GTSAM_USE_SYSTEM_EIGEN)前面加上set(GTSAM_USE_SYSTEM_EIGEN ON)，使得gtsam使用自己安装的eigen而不是它自带的eigen。然后重新编译gtsam，之后再编译LIO-SAM
