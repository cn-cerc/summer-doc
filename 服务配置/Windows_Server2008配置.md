# Windows
小图标任务栏
锁定任务栏
服务器管理器

### 配置IE ESC
- 管理员>关闭
- 用户>关闭

## 必备软件

## PS:建议以下软件使用使用浏览器下载，如果是国内服务器并且上传速度较快的话建议上传，如果可以科学上网建议下载

### Chrome
### https://www.google.com/chrome/

### Firefox
### https://download-ssl.firefox.com.cn/releases-sha2/stub/official/zh-CN/Firefox-latest.exe

### bandzip
http://www.bandisoft.com/bandizip/dl.php?web

### jdk1.8
https://download.oracle.com/otn-pub/java/jdk/8u201-b09/42970487e3af4f5aa5bca3f542482c60/jdk-8u201-windows-x64.exe
- 安装jdk
- 安装jre

### tomcat8.5
http://mirrors.shu.edu.cn/apache/tomcat/tomcat-8/v8.5.38/bin/apache-tomcat-8.5.38-windows-x64.zip
- 安装tomcat8.5

### maven3.6
http://mirrors.tuna.tsinghua.edu.cn/apache/maven/maven-3/3.6.0/binaries/apache-maven-3.6.0-bin.zip
- 安装maven3.6

### eclipse
https://www.eclipse.org/downloads/download.php?file=/technology/epp/downloads/release/2018-12/R/eclipse-jee-2018-12-R-win32-x86_64.zip&mirror_id=1281
- Eclipse配置
  具体配置请参考：https://github.com/cn-cerc/summer-doc/blob/develop/eclipse/Eclipse.md
- 字体
- 缩进
- 代码格式
- lombok.jar
导入lombok.jar，在lombok.jar文件夹路径中输入cmd打开命令提示符
输入java -jar lombok.jar进行安装
- 导入项目
具体配置请参考：https://github.com/cn-cerc/summer-training
- 更改端口
- 更改目录为/

### git
https://github.com/git-for-windows/git/releases/download/v2.21.0.windows.1/Git-2.21.0-64-bit.exe

### gitHub
https://central.github.com/deployments/desktop/desktop/latest/win32
- 克隆项目链接下载
- 打war包

### notepad++
https://notepad-plus-plus.org/repository/7.x/7.6.4/npp.7.6.4.Installer.exe

### Redis
https://github.com/MicrosoftArchive/redis/releases/download/win-3.2.100/Redis-x64-3.2.100.zip
- 启动redis-server

## 配置环境变量

### JAVA_HOME
```
#输入你的JDK路径，下面是做演示
C:\Program Files\Java\jdk1.8.0_201
```
### CLASSPATH
```
.;%JAVA_HOME%\lib
```
### MAVEN_HOME
```
#输入你的MAVEN路径，下面是做演示
C:\Users\l1091\Documents\i-tool\apache-maven-3.6.0
```
### PATH
```
;%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;%MAVEN_HOME%\bin
```

