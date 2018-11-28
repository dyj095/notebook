# 03_QT5.11_ms2017_32bit源码编译
[原文详见 简书 作者：觉醒的苍红之刃](https://www.jianshu.com/p/d0ce6f1dcf56)

> 这篇教程应用于Windows平台上要编译32bit的应用程序（包含Qt WebEngine模块）,由于Qt5.11中的WebEngine模块要求在Windows上必须得安装了VisualStudio2017(只有64bit)，QT安装的时候也只有一个ms2017 64bit的编译器，导致QT无法编译32bit的应用程序；解决方案就是手动将QT源码编译成32位的QT，也包括WebEngineView；
## 一、环境
1.VS 2017安装；<br>
2.[ActivePerl安装](http://www.perl.org/get.html)；<br>
3.[Python 2.7安装](https://www.python.org/ftp/python/2.7.11/python-2.7.11.msi)<br>
（不能用Python 3及以上版本，官方暂不支持）；
4.[Ruby安装](https://cache.ruby-lang.org/pub/ruby/2.3/ruby-2.3.1.tar.gz)；<br>
5.[icu](http://download.icu-project.org/files/icu4c/57.1/icu4c-57_1-Win32-msvc10.zip) <br>
解压即用，比如解压到C:\icu4c，并添加环境变量；<br>
6.[openssl](https://www.openssl.org/source/openssl-1.0.1t.tar.gz) <br>
（不要以为版本号看起来更高就下载那个openssl-1.0.2h.tar.gz，该版本不兼容！）
### 编译openssl流程如下：<br>
> 1.解压下载的openssl源码，比如解压到C:\openssl-1.0.1t ；<br>
> 2.打开“VS2017 开发人员命令提示“；<br>
> 3.执行命令<br>
>> ```shell
>> cd C:\openssl-1.0.1t 
>> perl Configure VC-WIN32 no-asm –prefix=C:\openssl-1.0.1t\win32dll
>> ms\do_ms
>> nmake -f ms\ntdll.mak
>> nmake -f ms\ntdll.mak install
>> ```
## 二、QT源码编译
1.下载Qt最新源码 [qt-everywhere-src-5.11.0-rc2.zip](https://download.qt.io/development_releases/qt/5.11/5.11.0-rc2/single/qt-everywhere-src-5.11.0-rc2.zip)<br>
2.解压；<br>
3.打开qt-everywhere-src-5.11.0-rc2\qtwebengine\src\3rdparty\chromium\third_party\skia\src\core\SkEdge.cpp，
找到第238行的
>> ```shell
>> // fCurveCount = SkToS8(1 << shift); 修改为
>> fCurveCount = SkToS8(1i64 << shift)//（已经不太确定这步是否需要）;
>> ```
4.打开 VS 2017的 x64_x86交叉工具命令提示符<br>
![图1](https://github.com/dyj095/notebook/blob/master/03_QT5.11_ms2017_32bit%E6%BA%90%E7%A0%81%E7%BC%96%E8%AF%91/imgs/1.webp)<br>
5.执行命令
>> ```shell
>> cd /d + 你的Qt源码路径
>> configure -debug-and-release -opengl desktop -make libs -nomake tests -nomake examples -mp
>> // 其中会出现两个选择，分别输入o回车确认（估计没有人是用花钱的，如果是，那么选择另外一项），y回车确认。
>> ```
6.执行命令<br>
> 因为我要确认qtwebengine是否能编译成功，故执行以下的命令，如果不需要确认则去掉后边的module-qtwebengine执行nmake即可
>> ```shell
>> nmake module-qtwebengine
>> ```
> 如果使用jom，则nmake替换成jom，jom是Qt官方工具，据说比nmake编译速度快
> [jom安装教程](https://www.jianshu.com/p/0e6c91317327)
> 如果是jom，那么执行
>> ```shell
>> jom module-qtwebengine
>> ```
> 等几个小时编译好，编译速度取决于电脑性能，最后执行命令
>> ```shell
>> nmake install
>> ```
7.完成后你会发现所有的东西都放在C盘Qt目录下了
![图2](https://github.com/dyj095/notebook/blob/master/03_QT5.11_ms2017_32bit%E6%BA%90%E7%A0%81%E7%BC%96%E8%AF%91/imgs/2.webp)

## 三、报错记录
### 1.模块计算机类型“x86”与目标计算机类型“x64”冲突
![图3](https://github.com/dyj095/notebook/blob/master/03_QT5.11_ms2017_32bit%E6%BA%90%E7%A0%81%E7%BC%96%E8%AF%91/imgs/3.webp)
### 2.内存不足
![图4](https://github.com/dyj095/notebook/blob/master/03_QT5.11_ms2017_32bit%E6%BA%90%E7%A0%81%E7%BC%96%E8%AF%91/imgs/4.webp)
以上两个问题的解决方案<br>
选择VS 2017的 x64_x86交叉工具命令提示符，这就是上边编译第四步选择该命令提示符的原因。
### 3.无法打开atl.lid
> #### 1.在程序中找到VS 2017，右键->更改
![图5](https://github.com/dyj095/notebook/blob/master/03_QT5.11_ms2017_32bit%E6%BA%90%E7%A0%81%E7%BC%96%E8%AF%91/imgs/5.webp)
> #### 2.选择ATL相关选项，执行修改,VS 2017组件附图
![图6](https://github.com/dyj095/notebook/blob/master/03_QT5.11_ms2017_32bit%E6%BA%90%E7%A0%81%E7%BC%96%E8%AF%91/imgs/6.webp)
![图7](https://github.com/dyj095/notebook/blob/master/03_QT5.11_ms2017_32bit%E6%BA%90%E7%A0%81%E7%BC%96%E8%AF%91/imgs/7.webp)
![图8](https://github.com/dyj095/notebook/blob/master/03_QT5.11_ms2017_32bit%E6%BA%90%E7%A0%81%E7%BC%96%E8%AF%91/imgs/8.webp)
![图9](https://github.com/dyj095/notebook/blob/master/03_QT5.11_ms2017_32bit%E6%BA%90%E7%A0%81%E7%BC%96%E8%AF%91/imgs/9.webp)
![图10](https://github.com/dyj095/notebook/blob/master/03_QT5.11_ms2017_32bit%E6%BA%90%E7%A0%81%E7%BC%96%E8%AF%91/imgs/10.webp)
![图11](https://github.com/dyj095/notebook/blob/master/03_QT5.11_ms2017_32bit%E6%BA%90%E7%A0%81%E7%BC%96%E8%AF%91/imgs/11.webp)
![图12](https://github.com/dyj095/notebook/blob/master/03_QT5.11_ms2017_32bit%E6%BA%90%E7%A0%81%E7%BC%96%E8%AF%91/imgs/12.webp)
![图13](https://github.com/dyj095/notebook/blob/master/03_QT5.11_ms2017_32bit%E6%BA%90%E7%A0%81%E7%BC%96%E8%AF%91/imgs/13.webp)
![图14](https://github.com/dyj095/notebook/blob/master/03_QT5.11_ms2017_32bit%E6%BA%90%E7%A0%81%E7%BC%96%E8%AF%91/imgs/14.webp)

