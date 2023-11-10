#启动容器

```shell
docker run -it <imagenames> /bin/bash
```

* `-i`使用交互式操作
* `-t`呼出终端
* `/bin/bash`希望使用bash进行交互式操作



想要退出终端,直接使用`exit`

想要退出非交互式容器,使用`docker stop <id or name>`

想要删除容器,使用`docker rm -f <id>`



## 使用容器运行web服务器

```shell
docker run -d -P  想要映射的端口:默认端口 <web server>
```

* `-d`让容器在后台运行
* `-p`设置映射端口到指定端口,如果你没有给指定端口,就随机分配



## 查看所有容器,包括已经停止的容器

```shell
docker ps -a
```



#使用镜像

## 获取镜像

```shell
docker pull <imagenames>
```



## 删除镜像

```shell
docker rmi <imagenames>
```

* 只有删除了运行镜像的容器,包括已经停止的容器,才可以删除images

## 更新镜像

```shell
在容器内部使用
apt-get update
```



## 构建镜像

```shell
# Specify Fedora Linux as base image
FROM fedora:latest

# Install Python with yum (Fedora's Package Manager)
# Install required Python packages
RUN yum update -y && yum install -y python3 python3-pip && \
    python3 -m pip install pyfiglet termcolor
 
# Add the missile.py file to the final image
ADD missile.py /

# Specify the command to be run on container creation
CMD ["/usr/bin/python3", "missile.py"]
```

* 我们需要创建一个Dockerfile文件,并使用`docker build`创建image
* 在命令行中使用`-t`指定创建的目标镜像名