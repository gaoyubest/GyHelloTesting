[TOC]

# JMeter安装

## JMeter下载

[JMeter官方下载链接](https://jmeter.apache.org/download_jmeter.cgi)

可以安装多个版本，下载完成后解压：

- bin：启动文件
- lib：依赖包
- licenses：证书
- extras：扩展包
- docs：api包、截图

## 配置环境变量

1、在安装Jmeter之前，先检查下电脑有没有装JDK：
cmd->进入命令行界面，输入java -version ，出现以下信息就是此电脑已安装了JDK

```bash
C:\Users>java -version

java version "1.8.0_231"
Java(TM) SE Runtime Environment (build 1.8.0_231-b11)
Java HotSpot(TM) 64-Bit Server VM (build 25.231-b11, mixed mode)


C:\Users>java -verbose

有关详细信息, 请参阅 http://www.oracle.com/technetwork/java/javase/documentation/index.html。
[Loaded java.lang.Shutdown from D:\Java\jdk1.8.0_231\jre\lib\rt.jar]
[Loaded java.lang.Shutdown$Lock from D:\Java\jdk1.8.0_231\jre\lib\rt.jar]
```

2、下载完成后，解压保存，配置环境变量

```bash
系统变量创建两个属性：
变量名：JMETER_HOME
变量值：D:\jmeter-5.4.1\apache-jmeter-5.4.1（存放位置）
变量名：CLASSPATH
变量值：%JMETER_HOME%\lib\ext\ApacheJMeter_core.jar;%JMETER_HOME%\lib\jorphan.jar;%JMETER_HOME%\lib\logkit-1.2.jar; （直接复制即可）
```

![](./images/07_JMter用户变量.png)

3、系统变量path后面加上%JMETER_HOME%\bin

![](./images/07_JMter系统变量2.png)

创建完成之后点击“确定”即可

## 打开JMeter

4、cmd命令行可查看是否安装成功，jmeter可打开。
或者点击jmter目录下bin中的jmeter.bat打开

```bash
C:\Users\Gaoyu>jmeter -v
    _    ____   _    ____ _   _ _____       _ __  __ _____ _____ _____ ____
   / \  |  _ \ / \  / ___| | | | ____|     | |  \/  | ____|_   _| ____|  _ \
  / _ \ | |_) / _ \| |   | |_| |  _|    _  | | |\/| |  _|   | | |  _| | |_) |
 / ___ \|  __/ ___ \ |___|  _  | |___  | |_| | |  | | |___  | | | |___|  _ <
/_/   \_\_| /_/   \_\____|_| |_|_____|  \___/|_|  |_|_____| |_| |_____|_| \_\ 5.4.1

Copyright (c) 1999-2021 The Apache Software Foundation


C:\Users\Gaoyu>jmeter
================================================================================
Don't use GUI mode for load testing !, only for Test creation and Test debugging.
For load testing, use CLI Mode (was NON GUI):
   jmeter -n -t [jmx file] -l [results file] -e -o [Path to web report folder]
& increase Java Heap to meet your test requirements:
   Modify current env variable HEAP="-Xms1g -Xmx1g -XX:MaxMetaspaceSize=256m" in the jmeter batch file
Check : https://jmeter.apache.org/usermanual/best-practices.html
================================================================================
```

压测工具：
LoadRunner偏向于业务；JMeter偏向于功能和技术
LoadRunner有强大的图表系统；JMeter这块弱一点
