# part1

```shell
systemctl //输出一串systemd列表

systemctl --type=service
//输出systemd中属于service的列表,即运行在系统上的服务
```



###Q1:要求我们使用nginx来访问web



```shell
sudo apt install nginx
sudo systemctl start nginx//启动
systemctl status nginx//查看是否运行
```



随后,要求我们更改nginx的默认启动端口

```shell
文件:/etc/nginx/sites-available/default

listen 80 default_server;
listen [::]:80 default_server;
改为
listen 420 default_server;
listen [::]:420 default_server;
```

* 需要给予权限
* 第一个是IPv4的配置
* 第二个是IPv6的配置



随后重启

```shell
sudo systemctl reload nginx
```



随后使用420访问网址

关闭

```shell
sudo systemctl stop nginx
```



###Q2:reload 和 restart的区别是什么?

my answer: reload只是重新装载了内存中的副本,而restart重新读取外存中的文件信息,两者有本质区别



###Q3:使用curl访问本地web,并创建一个服务

* `curl`是一个用于命令行界面的开源工具，用于传输数据，支持多种协议，包括 HTTP、HTTPS、FTP、SCP、SFTP 等。`curl` 允许用户通过命令行发出各种网络请求，例如下载文件、发送HTTP请求、测试API等等

____

**要求**我们安装`build-essential``make``python3-virtualenv`并且git一个文件decal-labs

```shell
# apt update
# apt install build-essential make python3-virtualenv
```



随后在我们git的decal-labs中,进入package 4

随后运行`./run`这个文件**注意,创建虚拟环境需要sudo权限**



这个shell文件创建了一个只能在本地访问的web服务器,浏览器输入localhost:5000会打开一个网页

____

**我们需要创建一个系统服务**来管理这个web server

给了我们代码框架

```shell
[Unit]
Description=
Requires=
After=

[Install]
WantedBy=multi-user.target
//这个部分指定了服务的安装相关信息，比如在哪里启用这个服务
[Service]
ExecStart=
User=
```



我给出的代码

```shell
 [Uint]
 Description=a unit file        [Install]
 WantedBy=multi-user.target 
 [Service]
 ExecStart=~/Desktop/decal-labs/4/run
 User=good
```



Q1:启动webserver之前需要启动什么东西?

A:After后的服务已启动,require中的依赖文件



Q2:启动服务会启动哪些脚本

A:脚本中所需要运行的脚本文件.即ExecStart后的文件



Q3:元数据经常以root身份运行,这安全吗?

____

接下来要求我们运行这个service并尝试使这个程序崩溃

```shell
curl -X POST -H "Content-Type: application/json" -d '{"crash":"true"}' http://localhost:5000/crash
```

结果:erro,错误代码显示被kill

原因:



____

Part1遇到的一些问题

Q1:nginx是什么?

A:Nginx是一个高性能的开源 Web 服务器和反向代理服务器，它以其卓越的性能、可靠性和灵活性而闻名。



Q2:service中的代码代表了什么

A:

```shell
[Unit]
Description=你的服务描述
Requires=某些必需的服务.target
After=某些必需的服务.target

[Install]
WantedBy=multi-user.target
//WantedBy 字段用于指定一个或多个 systemd 目标单元，这些目标单元在启动时依赖于当前服务单元。multi-user.target 是 systemd 的一个标准目标单元，它通常用于多用户系统的正常运行，类似于传统的运行级别。

[Service]
ExecStart=/路径/到/你的可执行文件 --一些选项
User=你的用户名
```

* 如果没有依赖,则为不写
* 在user中以exec的方式运行我设置的文件
* 我配置的文件必须是可运行文件

Q3:我修改了我的service文件,但是系统似乎没有reload

```shell
sudo systemctl daemon-reload
//需要我们手动reload
sudo systemctl restart toy.service
//尝试重启我的服务
```

`sudo systemctl daemon-reload` 命令用于重新加载 systemd 的配置，包括服务单元文件。当你修改了 systemd 服务单元文件时，需要运行这个命令，以使新的配置生效。



Q4:这个网页是用flask搭建的,什么是flask?

A:Flask 是一个用于构建 Web 应用程序的微型 Python Web 框架。它被设计成轻量级、简单且易于扩展的框架，使得开发者可以快速地创建 Web 应用程序和 RESTful API。



所以我们运行

```shell
sudo spt install python3-flask
```

以安装flask



Q5:part2中的网页似乎创建了虚拟环境

A:虚拟环境是用python的:`venv`模块创建的,如果虚拟环境已经存在`venv is up to date`,不会影响虚拟环境的开启



Q6:run中有一些代码`FLASK_APP=app.py exec flask run --host=0.0.0.0 `

A:告诉了flask的入口地址,使用`flask run`启动flask应用,并在localhost上监听请求,为什么浏览器在5000端口上访问网页呢?**因为flask默认端口为5000**



Q7:part2要求我们发送一个JSON负载给POST

A:

```shell
curl -X POST -H "Content-Type: application/json" -d '{"crash":"true"}' http://localhost:5000/crash
```

指定了请求方式为POST

`-H "Content-Type: application/json"`：设置请求头，告诉服务器请求体的格式为 JSON

`{"carsh":"true"}`为负载请求内容

* 我推测网页中有一个crash的标志位,当标志位为true的时候,就kill该进程
* 所以当我们发送json报文的时候,提示我们网站被kill了

* 后续是还真是

```python
def crash():
    if request.method == 'GET': 
        return 'You can either make a POST request to this endpoint with the json payload {"crash":"true"} (if you are cool) or you can use a command from lecture to manually kill the process'
    elif request.method == 'POST': 
        resp = request.get_json()
        if resp and 'crash' in resp:
            os.kill(os.getpid(), 9)
        return "You're on the right track! HINT: Pass content-type: application/json in the headers."
```



### 小结

该part给我们配置好了一个网页,并要求我们使用在nginx中打开这个网页.我们配置了一个系统service来执行这个网页.并要求我们post一段代码去kill它

____

# Part2

没有question

**该part要求我们了解htop**



学习`ps`命令

1. 使用ps查看进程

```shell
PID TTY          TIME CMD
 3371 pts/2    00:00:00 bash
 3416 pts/2    00:00:00 ps
```

2. 打开另一个terminal,并运行`sleep 1000 &`它会创建一个sleep进程,并告诉自己的PID

```shell
PID TTY          TIME CMD
 3371 pts/2    00:00:00 zsh
 3416 pts/2    00:00:00 ps
```

3. 当我们在第一个terminal中再次使用ps,会发现并没有sleep这个进程

4. 当我们使用ps -u时,会显示所有的进程,这个时候sleep进程出来了
5. 在linux中,每个终端都代表一个独立的终端会话,我们创建的进程,属于这个终端的子进程,并不会共享给终端1,这也与liunx中子进程的创建规则有关
6. 使用`ps -ef`查看所有进程

____

学习使用htop



1. htop是一个进程管理器,展示了所有运行的进程和他们的PID
2. F2将进入htop的设置
3. F5将以tree的形式展示程序
4. 使用`<`来查找你的程序

 

当我们在一个terminal创建sleep进程的时候,该进程为该terminal的子进程,当我们kill掉这个进程之后,会发现init进程(也就是系统进程)捕获了这个进程,该sleep进程现在是init进程的子进程了!

然而,当我们使用信号量**SIGHUP**删除一个进程时,这个进程会"顺便"kill掉它的所有子进程,也就是说,sleep进程也随之kill掉了



**有关信号量的知识需要深入研究**
