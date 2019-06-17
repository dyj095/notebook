# 03_QT5.11_ms2017_32bit源码编译
[原文详见 简书 作者：觉醒的苍红之刃](https://www.jianshu.com/p/d0ce6f1dcf56)

> 这篇教程应用于Windows平台上要编译32bit的应用程序（包含Qt WebEngine模块）,由于Qt5.12中的WebEngine模块要求在Windows上必须得安装了VisualStudio2017(只有64bit)，QT安装的时候也只有一个ms2017 64bit的编译器，导致QT无法编译32bit的应用程序；解决方案就是手动将QT源码编译成32位的QT，也包括WebEngineView；<br>
> Qt5.11编译失败，原因是在编译过程中由于VS2017 15.8 std::aligned_storage error导致编译中止，所以改为编译Qt5.12
## 一、环境
1.VS 2017安装；<br>
2.[ActivePerl安装](http://www.perl.org/get.html)；<br>
3.[Python 2.7安装](https://www.python.org/ftp/python/2.7.11/python-2.7.11.msi)<br>
（不能用Python 3及以上版本，官方暂不支持）；<br>
4.Ruby安装<br>
> 1.[Ruby源码下载](https://cache.ruby-lang.org/pub/ruby/2.3/ruby-2.3.1.tar.gz)；[Ruby Installer下载](https://github.com/oneclick/rubyinstaller2/releases/download/rubyinstaller-2.5.3-1/rubyinstaller-devkit-2.5.3-1-x86.exe)<br>
> 2.如果是下载完成后解压到本地（我解压到D:\program\ruby_src）
> 执行命令
>> ```shell
>> cd D:\program\ruby_src
>> win32\configure.bat i686-mswin32
>> nmake
>> nmake rubyw.exe//我在这步出现错误，所以改为下载rubyinstaller进行安装
>> namke test
>> nmake DESTDIR=D:\program\ruby install // 我的安装路径为D:\program\ruby
>> // 执行完成后，把D:\program\ruby\bin加入到PATH变量
>> ```
5.[icu](http://download.icu-project.org/files/icu4c/57.1/icu4c-57_1-Win32-msvc10.zip) <br>
解压即用，比如解压到C:\icu4c，并添加环境变量；<br>
6.[openssl](https://www.openssl.org/source/openssl-1.0.1t.tar.gz) <br>
（不要以为版本号看起来更高就下载那个openssl-1.0.2h.tar.gz，该版本不兼容！）
### 编译openssl流程如下：<br>
> 1.解压下载的openssl源码，比如解压到C:\openssl-1.0.1t ；<br>
> 2.打开“VS2017 开发人员命令提示“；<br>
> 3.打开 VS 2017的 x64_x86交叉工具命令提示符,执行命令<br>
>> ```shell
>> cd C:\openssl-1.0.1t 
>> perl Configure VC-WIN32 --prefix=D:\program\openssl
>> ms\do_ms
>> nmake -f ms\ntdll.mak
>> nmake -f ms\ntdll.mak install
>> ```
