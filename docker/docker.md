# 常用容器启动命令

## redis

下载镜像

```
docker pull redis
```

```
docker run --name some-redis -d redis
```

开机自启动

```
docker run --name **redis** -d -p 6379:6379 **--restart=always** redis
```

启用持久存储 

```
docker run --name some-redis -d redis redis-server --appendonly yes
```

## mysql

获取镜像

```
docker pull mysql
```
开机自启动

```
docker run --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root -d --restart=always mysql
```

Mysql 5.6.42
```
docker run --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root -d --restart=always mysql:5.6.42
```

## jenkins

获取镜像
```
docker pull jenkins/jenkins:lts
```

不指定数据卷
```
docker run --name jenkins -p 8080:8080 -p 50000:50000 jenkins/jenkins:lts
```

指定数据卷
```
docker run --name jenkins -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts
```

Jenkins密码地址
```
/var/jenkins_home/secrets/initialAdminPasswordMavne 插件
```
```
Maven Integration plugin
```

查看日志
```
docker logs jenkins
```

查看容器信息
```
docker inspect jenkins
```

联合执行

```
docker pull jenkins/jenkins:lts
docker stop jenkins && docker rm jenkins 
docker run --name jenkins -p 8080:8080 -p 50000:50000 --restart=always -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts
```

容器密码位置

```
/var/jenkins_home/secrets/initialAdminPassword
```

实际物理位置

```
/var/lib/docker/volumes/jenkins_home/_data
```

指定时区

```
docker run --name jenkins -p 8080:8080 -p 50000:50000 \--restart=always \-v /usr/share/zoneinfo/Asia/Shanghai:/etc/localtime \-v jenkins_home:/var/jenkins_home jenkins/jenkins:lts
```

Maven默认路径

```
/var/jenkins_home/tools/hudson.tasks.Maven_MavenInstallation/maven_3.6.1/conf
```

## rabbitMQ

获取镜像

```
docker pull rabbitmq:management
```

开机启动

```
docker run -d  -p 15672:15672  -p  5672:5672  -e RABBITMQ_DEFAULT_USER=admin -e RABBITMQ_DEFAULT_PASS=admin --restart=always --name rabbitmq rabbitmq:management
```

访问地址
[http://127.0.0.1:15672](http://127.0.0.1:15672/)