# 02_QT5.11_ms2017_32bit安装

[原文请详见](https://blog.csdn.net/star714/article/details/51340162)

## 一、资源下载 
[百度网盘](https://pan.baidu.com/s/1bpzj2QzXJa2NN2IKkn6fmQ),密码pvx7，[原文详见](https://blog.csdn.net/m0_37719965/article/details/81005764)
## 二、安装方法
### 1. 首先确认Qt动态库已经成功安装(官方默认安装动态库);
安装完成后 qmake.exe文件应在目录D:\Qt\Qt5.11.0\5.11.0\mingw53_32\bin中(也可以在其他分区盘中)
### 2. 将msvc2017静态库解压到QT动态库目录下
将下载的msvc2017_static.rar解压到Qt\Qt5.11.0\,代表动态库，解压完成后静态库的路径为：D:\Qt\Qt5.11.0\5.11.0\msvc2017_static，最后静态库qmake.exe文件应在目录D:\Qt\Qt5.11.0\5.11.0\msvc2017_static\bin中 
### 3. 添加qt.conf配置文件
在D:\Qt\Qt5.11.0\5.11.0\msvc2017_static\bin\下新建qt.conf，记事本打开并编辑：

[paths]

Prefix =D:/Qt/Qt5.11.0/5.11.0/msvc2017_static

保存格式必须为ANSI格式
### 4. 打开Qt Creator, 选择“工具”-> “选项”
左侧“构建和运行”界面中“Qt Versios”->“添加”，将静态库qmake.exe添加进去<br>
![效果图1](https://github.com/dyj095/notebook/blob/master/02_QT5.11_ms2017_32bit%E5%AE%89%E8%A3%85/imgs/1.png?raw=true)
添加完成有可能静态库前的三角标是红色“!”号，此时解决办法参考
http://www.cnblogs.com/andy65007/p/3493309.html
一般qt.conf没设置对，参考步骤3将qt.conf再次检查一遍
之后，“应用”->“确定”

### 5. 设置“构建套件”，选择“工具”-> “选项”
左侧“构建和运行”界面中“构建套件”->“添加”
手动设置栏下，自己设置名字，比如QtStatic
编译器、调试器、Qt版本如下设置
![效果图1](https://github.com/dyj095/notebook/blob/master/02_QT5.11_ms2017_32bit%E5%AE%89%E8%A3%85/imgs/2.png?raw=true)
之后，“应用”->“确定”


## 测试
### 1.测试：思想 , 动态库用来调试，静态库用来发布

“新建文件或项目”->“Qt Widgets Application”->“选择”<br>
![效果图3](https://github.com/dyj095/notebook/blob/master/02_QT5.11_ms2017_32bit%E5%AE%89%E8%A3%85/imgs/3.png?raw=true)

名称： testing   “下一步”<br>
![效果图4](https://github.com/dyj095/notebook/blob/master/02_QT5.11_ms2017_32bit%E5%AE%89%E8%A3%85/imgs/4.png?raw=true)

都选上，“下一步”<br>
![效果图5](https://github.com/dyj095/notebook/blob/master/02_QT5.11_ms2017_32bit%E5%AE%89%E8%A3%85/imgs/5.png?raw=true)

“下一步”直到完成<br>
![效果图6](https://github.com/dyj095/notebook/blob/master/02_QT5.11_ms2017_32bit%E5%AE%89%E8%A3%85/imgs/6.png?raw=true)

左下角“运行”三角按钮开始调试，此为动态库调试，运行成功的话就可以静态库调试发布了<br>
![效果图7](https://github.com/dyj095/notebook/blob/master/02_QT5.11_ms2017_32bit%E5%AE%89%E8%A3%85/imgs/7.png?raw=true)

静态库调试发布

Debug选择 Qstatic<br>
![效果图8](https://github.com/dyj095/notebook/blob/master/02_QT5.11_ms2017_32bit%E5%AE%89%E8%A3%85/imgs/8.jpg?raw=true)
