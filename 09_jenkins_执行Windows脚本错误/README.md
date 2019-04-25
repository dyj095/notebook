# 09_jenkins_执行Windows脚本错误
Jenkins编译后执行bat脚本将文件复制到windows共享目录下，在cmd下可以执行，但在Jenkins下执行bat就会报发生系统错误1312.
![img](https://github.com/dyj095/notebook/blob/master/09_jenkins_%E6%89%A7%E8%A1%8CWindows%E8%84%9A%E6%9C%AC%E9%94%99%E8%AF%AF/imgs/2.png)

## 1、解决方案
1、在”运行”中输入”services.msc”打开服务窗口，找到”Jenkins”
2、然后右键属性，在“登录”导航中选择“此用户”任何输入能够运行CMD.exe的用户。这里我用了管理员用户。
![img](https://github.com/dyj095/notebook/blob/master/09_jenkins_%E6%89%A7%E8%A1%8CWindows%E8%84%9A%E6%9C%AC%E9%94%99%E8%AF%AF/imgs/1.png)
