# What is Shell

* 允许你执行程序,输入并获取某种结构化的输出
* 是一种脚本语言,可以用来连接core和用户软件,且不用编译



# 一些常用commmands

```shell
echo //将程序打印出来
PATH  //环境变量,告知指令所在的目录
witch //告知程序所在位置
pwd //显示当前的工作目录
ls	//列出当前文件
> file //输入
< file //输出
>>		//向文件追加内容

pipe : | //管道允许我们将一个程序的输入和输出连接起来

sudo  //以管理员的身份运行程序

grep   //搜索字符
convent //复制文件
		convent xxx.jpg xxx.png
		==convent xxx.{png,jpg}
		

```



# shell中的语法变量,控制流以及函数



## " "是用于分隔参数的保留字符

```shell
foo=bar   //echo $foo ->bar
foo = bar //not found
```

## shell是如何在bash中处理字符串的?

```shell
echo "hello" == echo 'hello'
echo "value is $foo" -> value is bar
echo 'value is $foo'  -> value is $bar //单引号不处理变量
```



## shell中的特殊保留字符

```shell 
$#	//给定参数的个数
$$	//命令pid
$@	//储存所有参数

foo =$(pwd)	// 存入pwd的返回值
```



# 有用的软件

```shell
vim
tldr
tmux
ssh
shellcheck 
fdclone		//使命令渲染色彩
gcc
aunpack 	//解包软件  sudo apt install atool
neofetch    //显示各种配置(鲁大师)
```



