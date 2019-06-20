# 10_QT5.6.3源码编译

> 这篇教程应用于中标麒麟Linux64平台上要编译安装QT环境；<br>
> 安装linuxdeploy打包工具，以源码编译方式安装；Ubuntu请参见
[[04_QT程序发布_Ubuntu]](https://github.com/dyj095/notebook/tree/master/04_QT%E7%A8%8B%E5%BA%8F%E5%8F%91%E5%B8%83_Ubuntu/README.md)<br>
>将ubuntu16.04的qt编译环境，发布到没有qt环境的ubuntu16.04的机器上;采用的方式是linuxdeployqt命令方式<br/>
## 一、环境
1.[qt-everywhere-opensource-src-5.6.3.tar.xz](https://download.qt.io/archive/qt/5.6/5.6.3/single/qt-everywhere-opensource-src-5.6.3.tar.xz)；<br>
2.[linuxdeployqt SourceCode](https://github.com/probonopd/linuxdeployqt/releases)<br>

## 二、编译QT库
1.如果是下载完成后解压到本地（我解压到\diskE\qt\）
 执行命令
> ```shell
> cd \diskE\qt\
> tar -xvf qt-everywhere-opensource-src-5.6.3.tar.xz
> cd qt-everywhere-opensource-src-5.6.3
> // 安装完成以后安装到了/usr/local/Qt/Qt5.6.3
> ./configure -prefix=/usr/local/Qt/Qt5.6.3 -debug-and-release -nomake tests -nomake examples
> // 如果Qt应用程序有中文不显示的问题，可以改为下面的命令进行配置(需要添加fontconfig)
> ./configure -fontconfig -debug-and-release -qt-sql-sqlite -qt-zlib -qt-libpng -qt-libjpeg -qt-freetype -nomake tests -qt-xcb -nomake examples -prefix /usr/local/Qt/Qt5.6.3
> make -j4
> make install
> ```
2.设置环境变更 <br>
> ```shell
> vim /etc/profile
> // 将下面几行添加到/etc/profile 或~/.bashrc配置文件中
> export QTDIR=/usr/local/Qt/Qt5.6.3
> export PATH=$QTDIR/bin:$PATH
> export MANPATH=$QTDIR/man:$MANPATH
> export LD_LIBRARY_PATH=$QTDIR/lib:$LD_LIBRARY_PATH
> source /etc/profile
> // 或source ~/.bashrc
> ```

## 三、编译linuxdeploy
1.如果是下载完成后解压到本地（我解压到\diskE\qt\）
 执行命令
> ```shell
> cd \diskE\qt\
> tar -xvf linuxdeployqt-6.tar.gz
> cd linuxdeployqt-6
> qmake
> make
> make install
> ```

## 四、编译Qt工程
1.在Qt工程目录下执行命令
 执行命令
> ```shell
> cd \diskE\qt\QT_elink
> qmake QT_elink.pro -r -spec linux-g++ "CONFIG+=release" "CONFIG+=qml_release"
> make
> cd \diskE\qt
> mkdir elink_release
> cd elink_release
> cp \diskE\qt\QT_elink\elink\elink .\
> linuxdeployqt elink
> ```
