# 介绍

这是一个关于用pybind打包C++程序，给python使用的一个demo。
使用cmake编译。

# 使用

+ 新建build文件， `mkdir builld`
+ 进入build文件夹，`cd build`
+ cmake编译，生成.so文件
```
cmake ..
make
```
+ 进入plugin_test.py中，调用pybind11生成的python函数接口，实现python调用C++的函数实现