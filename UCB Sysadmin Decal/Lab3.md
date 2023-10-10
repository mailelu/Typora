# 下载debian

真的慢

插件介绍

* Xfce是一个轻量级的开源桌面环境,适用于低端硬件或者希望最大化性能用户的理想选择
* GNOME Flashback是一个用于Linux桌面环境的特殊模式或会话
* 

# 介绍Debian

Debian使用 `apt/dpkg`作为它的包管理器

## apt

从服务器上安装软件

```shell
sudo apt update//更新源
sudo search [package name] //寻找软件
sudo install[package]  
sudo remove [package]
sudo upgrade | sudoapt dist-upgrade  //更新软件

```

- `apt-get upgrade` will not change what is installed (only versions),
- `apt-get dist-upgrade` will install or remove packages as necessary to complete the upgrade,
- `apt upgrade` will automatically install but not remove packages.
- `apt full-upgrade` performs the same function as `apt-get dist-upgrade`.

以上是从网站上抄下来的关于"apt upgrade"和"apt dist-upgrade"的区别



```she
apt policy [package] //查看可选的安装版本
apt -t [版本] install [package]  //安装特定版本
```



## dpkg

与apt的区别:dpkg用来安装本地软件包

```shell
dpkg -i [packagefilename] //安装本地包
dpkg --remove[package]  //移除本地包
dpkg -I [package]  //了解更多关于包的信息
dpkg  --configure -a //修复或配置所有已解压但未安装成功的包
```



# debian遇到的一点困难



1. debian是没有桌面管理器的,也就一位置**你无法将像我们熟悉额windows一样将文件放在桌面**
2. 在你安装debian的时候,你设置了两个用户,一个是管理员用户,一个是普通用户也就是你登录进去的用户,也就意味着**你无法直接使用sudo**

```shell
su //以进入管理员模式
su  usermod -aG sudo 你的用户名//以将用户添加至管理员
```

3. 查看你使用的桌面名称

```shell
echo $DESKTOP_SESSION //众所周知,linux有许多桌面,各有特点
```

4. 当我们发现一个文件夹中有许多文件,但是没有某种权限,那么我有什么快捷的方法吗?

```shell
sudo chown -R <user> <filename> //将这个文件的所有权转移到用户(且启用递归)
chmod -R -i 目录名称 //给这个目录启动继承
```

5. 我想让虚拟机能使用我的vpn,我该怎么办?

​			answer:1.将虚拟机网卡改成:桥接模式并复制物理网络状态

​						  2.在系统中设置网络代理:ip地址为pc中ipv4地址,使用的端口为clash的端口

6. **这个时候我该怎么该回去?!!!**

我只能说这是一个玄学问题,因为我尝试了好几次都没用

但是我找了以下代码,好了

```shell
sudo /etc/init.d/networking restart && sudo dhclient
```

* 首先重启虚拟机
* 其次更改网络设置
* 然后sudo一下代码

这个故事告诉我们,要**保存网络快照!!**



# now it's lab time

## Exercise 1

第一个联系我们创建了一个c语言代码,并使用fpm创建了一个软件包

我们需要设定软件包的安装位置,于是创建了一个/usr/bin的文件夹

这个时候使用`fpm`代码创建用户包

```shell
fpm -s dir -t deb -n hellopenguin -v 1.0~ocf1 -C packpenguin
```

* 用户包在debian中一般在`/usr/bin` 中

* 注意你需要下载

* > `gcc`
  >
  >  `make`
  >
  > ``ruby-dev`(Ruby开发包或者库)  类似dev-c++ 
  >
  > `ruby-ffi`(使其能和C语言交互)

* 设置了包名,目标文件,版本号,生成文件名



随后我们使用sudo安装他

```shell
sudo dpkg -i ./hellopenguin_1.0~ocf1_amd64.deb
```



* 注意包名,不同的cpu使用不同的架构,包名也会有所区别



## Exercise 2

这个实验尝试让我们写一个软件并打包,但是我们要往里面写一些错误的信息

比如: 将 `/usr/bin`的文件夹创作为 `/usr/share`

​		这将导致我们安装后并不能运行我们想安装的软件,不i报错

此时`/usr/share`会多出你安装的文件



学习它的意义是什么呢?

For Hotshots
---

In the past examples, we have always precompiled a given program before packaging it. One upside to this, is that the package will always work for systems similar to the one that you run. However, once we start introducing other machines with potentially different architectures, we suddenly need to create duplicate packages compiled specifically for those systems. Create a new package that unpacks the source code for a file, compiles it, moves all of the relevant files to their respective locations, before deleting the irrelevant files.

(偷)



