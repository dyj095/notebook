# 07_QT_windows下使用MinGw编译出现中文乱码问题解决
[原文](https://blog.csdn.net/Timekeeperl/article/details/68266218)<br>
QT在Windows下如果采用MSVC2017_64编译器进行编译程序后，服务器返回的json中有中文显示也是正常的；但是如果采用Mingw_32编译器进行编译后，服务器返回的JSON中的所有中文显示都是乱码；

## 1、解决方案
在QT的工程文件中添加下面一行配置 
```cpp
CONFIG += -fexec-charset=GBK
CONFIG += -finput-charset=UTF-8
```
第一个参数指定窄字符或窄字符串的字面值常量的内部编码方式，默认为UTF-8。例如指定此选项为GBK，则窄字符或窄字符串常量将会以GBK编码方式存储而不是默认的UTF-8编码方式。

第二个参数，可能不需要加，加了第一个参数后还有乱码可以试试这个，意思是指定源文件的文件编码。
![img](https://github.com/dyj095/notebook/blob/master/07_QT_windows%E4%B8%8B%E4%BD%BF%E7%94%A8MinGw%E7%BC%96%E8%AF%91%E5%87%BA%E7%8E%B0%E4%B8%AD%E6%96%87%E4%B9%B1%E7%A0%81%E9%97%AE%E9%A2%98%E8%A7%A3%E5%86%B3/imgs/1.png)

## 2、如果你是直接编译
```shell
g++ -fexec-charset=GBK test.cpp -o test
```

## 3、如果使用codeblocks
就是给编译器加上选项：-fexec-charset=GBK，和windows默认的统一，就OK了。
