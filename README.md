# Docker 常用命令说明

## 基本概念
***

* 镜象
* 容器
* 仓库

## 冒烟测试
***

``` docker run hello-world ```

## 辅助命令
***
```
docker version  //docker客户端和服务端版本 
docker info 
docker --help 
```

## 常用命令
***
```
docker images //查看镜象列表
docker ps //查看容器

```

## 镜象基本操作
***

```
docker images 列出当前镜象
docker image ls 列出当前镜象
docker pull 下载镜象
docker search 搜索镜象
docker image rm 删除镜象（前提是当前镜象没有容器在运行）
docker image rm  -f 强制删除镜象，删除镜象的同时把对应的容器也删除
docker images = docker images -a 列出所有镜象
docker images -q 只列出镜象的id列表
docker images hello-world -q 列出所有hello-world的镜象id
docker image rm -f $(docker images hello-world -q) 删除所有hello-world镜象
```

## 容器的基本操作
***

### 运行容器
```
命令格式：
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

docker run 
    -p 8080:8080 端口映射
    -d 以守护进程的方式运行 --detach
    --name 指定容器名字

例：
docker run -it --name mytomcat -p 8080:8080 tomcat


docker run -d --name mytomcat -P tomcat 
    -d 表示后台运行
    -P 大写的P表示容器暴露出来的端口与宿主机的随机端口进行映射
```

### 查看容器
```
docker ps
    -a 查看所有容器，包括当前未运行的容器
    -q quiet静默显示结果（只显示容器id）
    -f 过滤条件

例：
docker ps -f name=mytomcat -aq 
以上命令列出所有名称为mytomcat的容器的id
```

### 停止|关闭|暂停|恢复容器
```
docker start|stop 容器名|容器id
docker pause|unpause 容器名|容器id
docker kill 容器名|容器id (强制停止)
```

### 删除容器
```
docker rm -f 容器名|容器id
docker rm -f $(docker ps -aq) 删除所有容器
docker rm -f $(docker ps -f name=mytomcat -aq) 删除名称为mytomcat的容器
```

### 查看容器内进程
```
docker top 容器名|容器id
```

### 查看容器内部细节
```
docker inspect 容器名|容器id
```

### 查看程序运行日志
```
docker logs 容器名|容器id
 -f 实时输出日志
```

### 进入容器
```
docker exec -it 容器名|容器id bash 进入容器，与容器的bash进行交互
```

### 文件拷贝
```
docker cp 容器id:路径 主机目录
docker cp 主机目录 容器id:路径
```

### 数据卷机制
```
使用绝对路径
docker run -v 宿主机数据卷:docker数据卷:ro
注：ro = read only

使用别名方式设置数据卷
docker run -v alias:docker数据卷路径
使用别名有个好处，如果容器不小心删除了，文件还在。可以重启挂起来。
```


### 将容器打包成新的镜象
```
docker commit
```

### 镜象备份和还原
```
docker save
docker load
```