# 03_QT5.11_ms2017_32bit源码编译
[原文详见 简书 作者：觉醒的苍红之刃](https://www.jianshu.com/p/d0ce6f1dcf56)

## 一、环境
### 1.VS 2017安装；
### 2.ActivePerl安装；
### 3.Python 2.7安装（不能用Python 3及以上版本，官方暂不支持）；
### 4.Ruby安装；
### 5.icu 解压即用，比如解压到C:\icu4c，并添加环境变量；
### 6.openssl （不要以为版本号看起来更高就下载那个openssl-1.0.2h.tar.gz，该版本不兼容！）
> 编译openssl流程如下：<br>
>> #### 1.解压下载的openssl源码，比如解压到C:\openssl-1.0.1t ；<br>
>> #### 2.打开“VS2017 开发人员命令提示“；<br>
>> #### 3.执行命令<br>
>>> ```shell
>>> cd C:\openssl-1.0.1t 
>>> perl Configure VC-WIN32 no-asm –prefix=C:\openssl-1.0.1t\win32dll
>>> ms\do_ms
>>> nmake -f ms\ntdll.mak
>>> nmake -f ms\ntdll.mak install
>>> ```
