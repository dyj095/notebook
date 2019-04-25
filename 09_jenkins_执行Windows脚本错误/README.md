# 09_jenkins_执行Windows脚本错误
Jenkins编译后执行bat脚本将文件复制到windows共享目录下，在cmd下可以执行，但在Jenkins下执行bat就会报发生系统错误1312.
![img](https://github.com/dyj095/notebook/blob/master/07_QT_windows%E4%B8%8B%E4%BD%BF%E7%94%A8MinGw%E7%BC%96%E8%AF%91%E5%87%BA%E7%8E%B0%E4%B8%AD%E6%96%87%E4%B9%B1%E7%A0%81%E9%97%AE%E9%A2%98%E8%A7%A3%E5%86%B3/imgs/1.png)

## 1、解决方案
1、在”运行”中输入”services.msc”打开服务窗口，找到”Jenkins”
2、然后右键属性，在“登录”导航中选择“此用户”任何输入能够运行CMD.exe的用户。这里我用了管理员用户。
![img](https://github.com/dyj095/notebook/blob/master/07_QT_windows%E4%B8%8B%E4%BD%BF%E7%94%A8MinGw%E7%BC%96%E8%AF%91%E5%87%BA%E7%8E%B0%E4%B8%AD%E6%96%87%E4%B9%B1%E7%A0%81%E9%97%AE%E9%A2%98%E8%A7%A3%E5%86%B3/imgs/1.png)
