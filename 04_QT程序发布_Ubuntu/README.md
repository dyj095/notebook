# 04_QT程序发布_Ubuntu
[原文](http://www.cnblogs.com/feiyufu/p/9322106.html)<br>
将ubuntu16.04的qt编译环境，发布到没有qt环境的ubuntu16.04的机器上。<br>
有两种方式，一种是手动打包，需要将所需的库导出等。第一种是是用打包工具linuxdeployqt，本文采用第二种。<br>

## 1、下载已经编译好的版本 
[[点击下载]](https://github.com/probonopd/linuxdeployqt/releases)
![img](https://github.com/dyj095/notebook/blob/master/04_QT%E7%A8%8B%E5%BA%8F%E5%8F%91%E5%B8%83_Ubuntu/imgs/1.png)
## 2、下载完成后 进入下载好的目录，将其重命名
```shell
sudo mv linuxdeployqt-continuous-x86_64.AppImage linuxdeployqt
```

## 3、将重新命名好的文件，移动到/usr/local/bin
```shell
mv ./linuxdeployqt /usr/local/bin/
```

## 4、执行linuxdelpoyqt --version查看版本
```shell
linuxdeployqt --version
```
![img](https://github.com/dyj095/notebook/blob/master/04_QT%E7%A8%8B%E5%BA%8F%E5%8F%91%E5%B8%83_Ubuntu/imgs/2.png)

## 5、测试一下qmake
此时会提示：No such file or directory
需要设置下环境变量
```shell
vim ~/.bashrc

export PATH=/opt/Qt5.6.3/5.6.3/gcc_64/bin/:$PATH
```
保存退出后执行
```shell
source ~/.bashrc
qmake
```
![img](https://github.com/dyj095/notebook/blob/master/04_QT%E7%A8%8B%E5%BA%8F%E5%8F%91%E5%B8%83_Ubuntu/imgs/4.png)
此时qmake执行正常，至此，linuxdeployqt安装完成
## 6、发布
```shell
cd /home/hxyl/Desktop/elink/
linuxdeployqt elink
```
![img](https://github.com/dyj095/notebook/blob/master/04_QT%E7%A8%8B%E5%BA%8F%E5%8F%91%E5%B8%83_Ubuntu/imgs/5.png)
