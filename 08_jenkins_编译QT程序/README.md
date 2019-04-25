# 08_jenkins_编译QT程序

[原文](https://www.badprog.com/c-qt-framework-using-jenkins-to-generate-an-exe-file)<br>
通过Jenkins在Windows上使用mingw编译器对Qt程序进行编译生成exe<br>

## 一、环境说明
1、Jenkins [[下载]](https://jenkins.io/zh/)<br>
2、Qt_5.6.3(qt-opensource-windows-x86-mingw492-5.6.3) 


## 配置任务

5、add Build Step<br>
【Add Build Step】->【执行Windows批处理命令】<br>
在【Command】输入框内输入以下批处理指令
```shell
:: BadproG.com
:: =====================
:: Generating Makefile |
:: =====================

"D:/qt/Qt5.6.3/5.6.3/mingw49_32/bin/qmake.exe" D:/elink/Jenkins/workspace/QT_elink/QT_elink.pro -spec win32-g++ "CONFIG+=debug" "CONFIG+=qml_debug" && D:/qt/Qt5.6.3/Tools/mingw492_32/bin/mingw32-make.exe qmake_all

:: ===========
:: Compiling |
:: ===========

rem "D:/qt/Qt5.6.3/Tools/mingw492_32/bin/mingw32-make.exe" -f D:/elink/Jenkins/workspace/QT_elink/Makefile.Debug

:: ======================================
:: Moving .dll to the project directory |
:: ======================================

rem copy "D:\qt\Qt5.6.3\5.6.3\mingw49_32\bin\Qt5Cored.dll"       D:\elink\Jenkins\workspace\QT_elink\debug\Qt5Cored.dll
rem copy "D:\qt\Qt5.6.3\5.6.3\mingw49_32\bin\Qt5Widgetsd.dll"    D:\elink\Jenkins\workspace\QT_elink\debug\Qt5Widgetsd.dll
rem copy "D:\qt\Qt5.6.3\5.6.3\mingw49_32\bin\Qt5Guid.dll"        D:\elink\Jenkins\workspace\QT_elink\debug\Qt5Guid.dll
rem copy "D:\qt\Qt5.6.3\5.6.3\mingw49_32\bin\libgcc_s_dw2-1.dll" D:\elink\Jenkins\workspace\QT_elink\debug\libgcc_s_dw2-1.dll
rem copy "D:\qt\Qt5.6.3\5.6.3\mingw49_32\bin\libstdc++-6.dll"    "D:\elink\Jenkins\workspace\QT_elink\debug\libstdc++-6.dll"

rem copy "D:\qt\Qt5.6.3\5.6.3\mingw49_32\bin\libwinpthread-1.dll"    "D:\elink\Jenkins\workspace\QT_elink\debug\libwinpthread-1.dll"
```
