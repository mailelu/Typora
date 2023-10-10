# Packages



# Debian

since 1993,是最为稳定的一个版本



# 软件包

什么是软件包?

* 类似windows的exe文件,我们可以双击运行其中的命令,然后install on your computer
* 集中式包管理器:for safe
* 以更新安全补丁
* 软件包也可能依赖于其他的软件,譬如minecraft依赖java



# 安装软件包

```shell
sudo apt update  //sudou获取root权限
sudo apt install
sudo apt remove
```





```shell
apt dist-upgrade
apt search <packagename>
apt install ,.package.deb
//安装本地包(又或者是你自己的代码)
```





安装本地安装包是不安全的,安装位于数据库中的软件包是经过审查的

  

# 软件包的形成步骤

源码->可执行文件->封装



# 什么是编译?

将源码转换成可执行文件



# 关于make

使用make创建可执行文件,即编译代码,类似运行一段自动安装的脚本



# 如何制作一个软件包?

```shell
sudo apt install fuby-dev
sudo gem install fpm
fpm -s dir -t deb -n [name here] -v [version #] -c [the directory with the /usr folder]
```

#关于md5(差错检测)

类似哈希值,当你下载文件时,为了不让文件出错,会使用md5sums检错,是一种很古老的检查方法,所以不是很安全(但是兼容性足够)



